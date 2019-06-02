---
title: ECMAScript-Learning
tags:
  - Node.js
description: 使用ES6, 实际上是混用ES5和ES6
categories:
  - Experience
date: 2019-06-02 21:25:51
---

# 前言
>[ES6](https://zh.wikipedia.org/zh-cn/ES6):
 ECMAScript 2015（ES2015），第 6 版，最早被称作是 ECMAScript 6（ES6），添加了类和模块的语法，其他特性包括迭代器，Python风格的生成器和生成器表达式，箭头函数，二进制数据，静态类型数组，集合（maps，sets 和 weak maps），promise，reflection 和 proxies。作为最早的 ECMAScript Harmony 版本，也被叫做ES6 Harmony。 

>在知道了ES6仍未实现之后，我始终暗示自己存在一种方法，使得可以避免使用ES5
 然后不停地寻找，最后发现这并不能实现，必须需要一个index之类的文件用于启动，而它必须只能是ES5的
 当然，它可以只有几条语句: 导入主方法，运行主方法，这之后只需要在主方法中使用ES6即可
 而ES6本身**主要**只是强化了类这一概念而已，然后就是模块的导入方法不同，当前的模块导入并非是官方实现的

## [CommonJS](www.commonjs.org/) Node.js

如果是看过相关代码的话, 极有可能被这几个概念弄昏头, 此处直观地区分一下:
> - const, let 是ES5的内容
  - **require**是**CommonJS**的内容 `这一点下面会详细分析`
  - CommonJS是**Node.js**平台的内容
  - Node.js使用Chrome的**V8引擎**

[关于AMD,CMD,CommonJS及UMD规范](https://www.tuicool.com/articles/nueqi27)
[关于 CommonJS AMD CMD UMD 规范的差异总结](https://www.cnblogs.com/imwtr/p/4666181.html)

## 区分
`引用原文`[模块导入 require，import的区别](https://www.zhihu.com/question/56820346)
>require/exports 出生在野生规范当中，什么叫做野生规范？即这些规范是 JavaScript 社区中的开发者自己草拟的规则，得到了大家的承认或者广泛的应用。比如 CommonJS、AMD、CMD 等等。
  import/export 则是名门正派。TC39 制定的新的 ECMAScript 版本，即 ES6（ES2015）中包含进来。
  `本人注: 不论前边多花哨, require里边以及from后边的引号是必须的, 该字符串实质上是一个路径(绝对/相对)`
  ```js
  // require/exports 的用法只有以下三种简单的写法
  const fs = require('fs')

  exports.fs = fs
  module.exports = fs

  // 而 import/export 的写法就多种多样：import fs from 'fs'
  import {default as fs} from 'fs'
  import * as fs from 'fs'
  import {readFile} from 'fs'
  import {readFile as read} from 'fs'
  import fs, {readFile} from 'fs'

  export default fs
  export const fs
  export function readFile
  export {readFile, read}
  export * from 'fs'
  ```
> _
  1. CommonJS 还是 ES6 Module 输出都可以看成是一个具备多个属性或者方法的对象；
  2. default 是 ES6 Module 所独有的关键字，export default fs 输出默认的接口对象，import fs from 'fs' 可直接导入这个对象；`本人注: 一般情况下是需要解构赋值的`
  3. ES6 Module 中导入模块的属性或者方法是强绑定的，包括基础类型；而 CommonJS 则是普通的值传递或者引用传递。

## 实操
`ES6`Point.js
```js
export default class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }
}
```

若在ES6中则按照ES6规范正常导入即可
`ES6`Line.js
```js
// import Point from Point; // 同样需要使用解构赋值
// import {Point} from Point; // 引号
// import {Point} from 'Point'; // 编译通过&&运行失败(Cannot find module 'Point') 是基于字符串查找实现的
import Point from './Point'; // ok

export class Line {
    constructor(xO, yO, xT, yT) {
      this.origin = new Point(xO, yO);
      this.target = new Point(xT, yT);
    }
  
    toString() {
      return '(' + this.origin.toString() + ', ' + this.target.toString() + ')';
    }
}
```

关于上述第2点, 使用 require 导入 ES6 的 export 时 需要
`ES5`index.js
```js
// import Point from /lib/Point; // 此处并不能使用ES6(而且语法还错了)
// const Point = require("./lib/Point"); // 不使用解构赋值是不行的
/* 
若使用 export default class ClassName 但仍使用解构赋值的话
则 编译会通过, 但会在首次使用 new ClassName 的地方line[14]提示错误:
  TypeError: ClassName is not a constructor
*/
const Point = require("./lib/Point").default; // 引用babel编译后的ES5
const {Line} = require("./lib/Line");


console.log("hello");

let po = new Point(1, 2);
let pt = new Point(3, 4);

console.log(po.toString());
console.log(new Line(po.x, po.y, pt.x, pt.y).toString());
```

`参考-1`[ECMAScript 6 入门](https://es6.ruanyifeng.com/#docs/class)
`参考-1`[Module 的语法](https://es6.ruanyifeng.com/#docs/module)
`参考`[ES6：export default 和 export 区别](https://www.jianshu.com/p/edaf43e9384f)
`参考`[exports、module.exports和export、export default到底是咋回事](https://segmentfault.com/a/1190000010426778)
`参考, GK: {babel 编译 export default  使用require导入; exports.default require}`[import、require、export、module.exports 混合使用详解](https://juejin.im/post/5a2e5f0851882575d42f5609)


## [Babel](https://www.babeljs.cn/docs/usage)
`参考-1`[Babel-转码器](https://es6.ruanyifeng.com/#docs/intro#Babel-%E8%BD%AC%E7%A0%81%E5%99%A8)
>Babel 是一个 JavaScript 编译器
 Babel 是一个工具链，主要用于将 ECMAScript 2015+ 版本的代码转换为向后兼容的 JavaScript 语法，以便能够运行在当前和旧版本的浏览器或其他环境中。
- 编译后的js代码使用严格模式可能是因为编译后的文件的名称可能会造成命名冲突

## 结语
一句话, ES6并未实现, 是babel编译器将ES6编译为ES5, 所以当下必须使用一个引导, 此引导需使用ES5, 当然它可以引用**编译后的ES5代码**
