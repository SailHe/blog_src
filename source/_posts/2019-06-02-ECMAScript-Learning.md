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
  - Node.js使用chromium的**V8引擎**

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


>注意, 若前后端都使用js的话极易引起混淆
1. 基于node.js的后端的js原本就可以导入导出模块, 只是想要使用ES6的话就得使用bable之类的编译器
2. {Vue, React, Angular, Backbone} 是**前端框架**, 目前**前端**的主体是 HTML5 和 CSS3, 当然 HTML和CSS只是**最终目标**, 而不是这些框架本身的实现
3. {swig} 是 **HTML模板引擎**, JSX 是使用 XML 语法编写 JavaScript 的一种语法糖。并不是HTML模板
4. {acss} 是 **CSS模板引擎**
5. 前端框架**一般**包括默认的或允许自定义HTML和CSS的模板引擎, 这就是**误解的源头**, 在啥也不了解的时候, 可能会觉得前端框架就是那些引擎本身, 而框架实质上只是技术的组合
6. 若想在前端写js的时候向node后端一样导入导出模块, 则需要引入**第三方用于解决依赖的js插件**, 可能还需要遵循一定的语法
7. [React](https://zh.wikipedia.org/wiki/React)（有时叫React.js或ReactJS）是一个为数据提供渲染为HTML视图的开源**JavaScript 库**。
8. [Vue](https://zh.wikipedia.org/wiki/Vue.js)Vue.js（/vjuː/，或简称为Vue）是一个用于创建用户界面的开源**JavaScript框架**，也是一个创建单页应用的Web应用框架。AngularJS 是 Vue 早期开发的灵感来源
9. 在传统的WEB前端中, 工程师需要组合各种**HTML标签**来达到某种效果
10. 在使用了React后, 这些标签可以组合起来, 形成一个**组件**, 利用HTML本身就可以使用js动态添加的特性, 进行所谓的**渲染**, 因此在 React 中，一切都是 JavaScript。[前端框架的对比](https://cn.vuejs.org/v2/guide/comparison.html)
11. Weex 是使用流行的 Web 开发体验来开发高性能原生应用的框架。[官网概述](https://weex.incubator.apache.org/zh/guide/introduction.html#概述)如是说 `不清楚是否更改+字都认识系列`
```Vue
// 为了更好地适应复杂的项目，Vue支持以.vue为扩展名的文件来定义一个完整组件，用以替代使用Vue.component注册组件的方式。开发者可以使用 Webpack或Browserify等构建工具来打包单文件组件。
Vue.component('buttonclicked', {
  props: [
    'initial_count'
  ],
  data() {
    return {
      count: 0
    }
  },
  template: '<button v-on:click="onclick">Clicked {{ count }} times</button>',
  methods: {
    onclick() {
      this.count += 1;
    }
  },
  mounted() {
    this.count = this.initial_count;
  }
});
```

```React
import React, { Component } from 'react';
import { render } from 'react-dom';

class HelloMessage extends Component {
  render() {
    return <div>Hello {this.props.name}</div>;
  }
}

// 加载组件到 DOM 元素 mountNode
render(<HelloMessage name="John" />, mountNode);
```

11. [Webpack](https://zh.wikipedia.org/wiki/Webpack) 是一个开源的前端打包工具。**Webpack 提供了前端开发缺乏的模块化开发方式**，将各种静态资源视为模块，并从它生成优化过的代码。
以下引用自[原文](https://www.webpackjs.com/concepts/modules/)
> 什么是 webpack 模块
 对比 Node.js 模块，webpack 模块能够以各种方式表达它们的依赖关系，几个例子如下：
    ES2015 `import` 语句
    CommonJS `require()` 语句
    AMD `define` 和 `require` 语句
    css/sass/less 文件中的 @import 语句。
    样式(`url(...)`)或 HTML 文件(`<img src=...>`)中的图片链接(`image url`)

12. 也就是说, Webpack整合了包括之前介绍过模块导入方法在内的几乎所有方法, 并且, 为前端开发提供了模块化开发方式, 也就是说Tips[6]提到的第三方插件已经没有存在的必要了
13. 上述所有一切都是为了**解决依赖**
14. Webpack的原理大概就是分析所有依赖语句, 然后合成到一个文件中
15. 由于HTML动态的部分也包含在JS里面了, 因此, 传统WEB中每个页面都包含的复杂HTML元素现在几乎就剩只有一个id为'root'的div了, 所有元素都是后期渲染上去的
16. Webpack与HTML模板的区别在于 前者是动态添加DOM元素, 类似于在页面引入一个js, js里边添加所有元素; 而后者是基于模板生成HTML, 类似于复用DOM; **这两者都是静态页面**;
17. **静态页面**表示没有后端, 不是指没有动态(DOM元素的变化)
18. **动态页面**的页面**可以是**在后端实时生成后返回给前端的


 以下都依赖于Node.js, 这一基于MIT开源的**跨平台JavaScript运行环境**

|    名称    | 主要技术依赖  |       解决的问题        |        类型         |             原作者+开发者             | 语言       |    初版    | 许可协议 |
| :-------: | :----------: | :--------------------: | :----------------: | :----------------------------------: | :--------- | --------- | ------- |
|  Webpack  |   Node.js    | 资源加载/模块化-解决依赖 |     前端打包工具     |          Tobias Koppers...           | JavaScript | 2012年03月 | MIT     |
|   React   | Webpac; kJSX | 跨平台渲染数据为HTML视图 |     前端渲染库      | Jordan Walke+Facebook+Instagram+社区 | JavaScript | 2013年03月 | MIT     |
| AngularJS |   Node.js    | 协助单页Web应用程序运行  |     前端库(MVC)     | Miško Hevery+Adam Abrons+Google+社区 | TypeScript | 2010年10月 | MIT     |
|   Weex    | Webpack; Vue |    跨平台用户界面开发    |        框架         |           阿里巴巴发起+社区           | JavaScript | 2016年--月 | Apache  |
|    Vue    |   Node.js    |      创建用户界面       | 前端/单页Web应用框架 |               Evan You               | JavaScript | 2014年02月 | MIT     |
| Electron  |   Chromium   |   桌面GUI应用程序开发    |      软件框架       |                GitHub                | 多种       | 2013年7月  | MIT     |

>宏观概念的区别
    - **[库](https://zh.wikipedia.org/wiki/函式庫)**(Library )是用于开发软件的子程序集合。库和可执行文件的区别是，库不是独立程序，他们是向其他程序提供服务的代码。**工具集合**
    - **[框架](https://zh.wikipedia.org/wiki/軟體框架)**(Framework)通常指的是为了实现某个业界标准或完成特定基本任务的**软件组件规范**; 也指为了实现某个软件组件规范时，提供规范所要求之基础功能的软件产品, 此时功能类似于**基础设施**。
    - **[架构](https://zh.wikipedia.org/wiki/软件架构)**(Architecture)是有关**软件整体结构**与**组件**的抽象描述，用于指导大型软件系统各个方面的设计。不是[计算机系统结构](https://zh.wikipedia.org/wiki/计算机系统结构)
    - **[平台](https://zh.wikipedia.org/wiki/系统平台)**是指在计算机里让软件运行的**系统环境**，包括硬件环境和软件环境。是能做的最根本的几件事的集合, 加法->高数以下(减法可补码, 积分类加, 微分类减),微信->小程序; 浏览器->Web应用; JVM->Java程序

>不恰当的理解:
>**函数**的实现往往依赖于特定的**数据结构** (否则实现起来或比较繁琐)
>**算法**是函数的核心(业务逻辑算..吧)
>**方法**是仅用于操纵数据结构的**内部数据**的函数
>**类**是**封装**了方法的数据结构, 用方法体现**行为**, 用内部数据体现**状态**
>函数的集合 称库
>库   的组合 称框架, 库之间通过**接口**连接


编程方法学

|        [编程范式](https://zh.wikipedia.org/wiki/编程范式)        |   将程序视为   |          基础           |
| -------------------------------------------------------------- | ------------ | ---------------------- |
| [面向对象程序设计](https://zh.wikipedia.org/wiki/面向对象程序设计) | 相互作用的对象 | {封装, 多态, 抽象, 继承} |
| [函数式程序设计](https://zh.wikipedia.org/wiki/函数式编程)        | 函数计算的序列 | {lambda运算, 闭包}      |


>框架与库之间最本质区别在于控制权
>you call libs (函数调用)
>frameworks inject you (控制反转后的依赖注入)
>React+Flux+react-router+react-redux 是 框架

[Electron](https://zh.wikipedia.org/wiki/Electron)(原名为Atom Shell) 是GitHub开发的一个开源框架。
著名项目
- Github客户端
- Atom
- Visual Studio Code
- MongoDB Compass
- [Unity](https://zh.wikipedia.org/wiki/Unity_(游戏引擎))

Repository
[Electron](https://github.com/electron/electron)
[React](https://github.com/facebook/react)
其它的就看Wiki好了..就不多列举了

## 关于跨平台
正因为Node.js本身是跨平台的, 这俩框架才有跨平台的可能, 但两者间并没有直接联系, Node.js跨平台直接决定了依赖于它的软件能够在不同的平台上构建(指Linux和Win)
指跨移动端{Android, iOS}和WEB, 而且是一次编写(只能算减少工作量)

- React Native(RN) 所有东西本就是JS
- Weex是将 .vue ,  .we 文件编译成 JS
- [Weex](https://zh.wikipedia.org/w/index.php?title=Special:%E6%90%9C%E7%B4%A2&search=Weex&ns0=1), apache, MYZ 了解一下
- RN毕竟更成熟(时间上+网评+社区), 之前花了好久才编译出一个基于RN的App: [BoostNote](https://github.com/BoostIO/boostnote-mobile), 效果却奇差无比, 估计试图开发完全跨平台的程序很难, 另外得提一下, [BoostNote](https://github.com/BoostIO/Boostnote) 好歹是正儿八经的跨平台呀, 不过之前做过测评, 最终没用这个, 个人认为其架构{electron; react}值得借鉴
- 某种意义上来说JS本身就是跨平台的(都有浏览器吧), 只是支持程度不同, 所以要搞兼容
- Java也说过一次编写到处运行, 不过它靠的是JVM虚拟机

组件化：webComponent; polymer; x-tag; react; jQuery-plugin; angular-directive
模块化:  webpack; browserify; require.js; sea.js
开发效率：MVC(Backbone) < Flux(React) < [MVVM](https://zh.wikipedia.org/zh-hans/MVVM)(Angular.js; vue; ember.js)
运行效率：Backbone; React
可维护性：Flux; Redux

[webpack 解决的痛点](https://www.jianshu.com/p/132b6d171647)
[Weex从入门到超神（一）](https://www.gaoshilei.com/2017/05/26/weex-1/)
