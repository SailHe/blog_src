---
title: Node.js-Learning
description: Node.js 相关的技能学习笔记
date: 2019-05-19 22:39:50
tags:
    - Node.js
categories:
    - Induction
---

# npm

npm是一个node包管理和分发工具，已经成为了非官方的发布node模块（包）的标准。
有了npm，可以很快的找到特定服务要使用的包，进行下载、安装以及管理已经安装的包。

```shell

# node的安装分为全局模式和本地模式
npm install moduleNames # 本地安装Node模块包 安装完毕后会产生一个node_modules目录，所有包会被安装到该目录下。
npm install -g moduleName # 全局安装Node模块 包会被安装到Node的安装目录下的node_modules下。
npm set global=true # 可用于设定安装模式
npm get global # 可查看当前使用的安装模式。

npm install # 根据dependencies配置安装所有的依赖包(代码提交到远端时，无需提交node_modules里的内容。)
npm install --save # 安装的同时，将信息写入package.json中项目路径中(若存在的话)
npm install -g # 将包安装到全局环境中，但代码中，直接通过require()是无法调用全局安装的包的。这些包可供命令行使用，如: 全局安装了vmarket后，就可在命令行中直接运行vm命令
npm install express # 默认会安装express的最新版本，也可以通过在后面加版本号的方式安装指定版本，如npm install express@3.0.6

npm view moduleNames # 查看node模块的package.json文件夹
npm view moduleName labelName # 查看package.json文件夹下某个标签的内容
npm list # 查看当前目录下已安装的node包
# 注意事项：Node模块搜索是从代码执行的当前目录开始的，搜索结果取决于当前使用的目录中的node_modules下的内容。
npm list parseable=true # 以目录的形式来展现当前安装的所有node包
npm help # 查看帮助命令
npm view moudleName dependencies # 查看包的依赖关系
npm view moduleName repository.url # 查看包的源文件地址
npm view moduleName engines # 查看包所依赖的Node的版本
npm help folders # 查看npm使用的所有文件夹
npm rebuild moduleName # 用于更改包内容后进行重建
npm outdated # 检查包是否已经过时，此命令会列出所有已经过时的包，可以及时进行包的更新
npm update moduleName # 更新node模块
npm uninstall moudleName # 卸载node模块

# 一个npm包是包含了package.json的文件夹，package.json描述了这个文件夹的结构。访问npm的json文件夹的方法如下：
npm help json # 此命令会以默认的方式打开一个网页，如果更改了默认打开程序则可能不会以网页的形式打开。
npm search packageName # 发布一个npm包的时候，需要检验某个包名是否已存在
npm init # 会引导你创建一个package.json文件，包括名称、版本、作者这些信息等
npm root # 查看当前包的安装路径
npm root -g # 查看全局的包的安装路径
npm -v # 查看npm安装的版本
```

更多命令参见[npm官方文档](https://www.npmjs.org/doc/)

* [React](https://react.docschina.org/docs/hello-world.html)


# [Weex](https://github.com/weexteam/weex-toolkit)
```shell
npm install -g weex-toolkit@latest # 安装
weex create your_project_name # 创建项目
cd path # 进入工程目录
cnpm install # 安装第三方依赖
cnpm run dev # 开启调试
npm start # 运行
```
如果在创建时选择了非自动安装的选项，在运行npm start 前需先运行 npm install

[Weex环境搭建(weexpack篇)](https://www.jianshu.com/p/a5efbbf080d7)

[一些常见错误](https://segmentfault.com/q/1010000009259256)


# 常用库
[lodash](https://lodash.think2011.net/)
[lodash-repo]()一个 JavaScript 的实用工具库, 表现一致性, 模块化, 高性能, 以及 可扩展，它使用函数式编程范例为常见的编程任务提供实用程序功能。
[faker-npm](https://www.npmjs.com/package/faker)用于在浏览器和node.js中生成大量虚假数据

[代理解决mock数据。](https://www.cnblogs.com/y896926473/articles/7437343.html)

[用于为数字值添加千位分隔符的包。](https://github.com/gejiawen/bullhead)
[基于Webpack的库的生成模板（输入：ES6，输出：通用库）](https://github.com/krasimir/webpack-library-starter)
[通用模块定义UMD-repo](https://github.com/umdjs/umd)
- Github Gist 2018-11-07左右

## Blog
[Sample Gruntfile](https://gruntjs.com/sample-gruntfile)
[Nodejs学习笔记（五）--- Express安装入门与模版引擎ejs](https://www.cnblogs.com/zhongweiv/p/nodejs_express.html)
[npm安装慢，换用淘宝的镜像](http://www.cnblogs.com/xueweihan/p/5491730.html)
[webpack-起步](https://webpack.docschina.org/guides/getting-started/#%E5%9F%BA%E6%9C%AC%E5%AE%89%E8%A3%85)
[JavaScript中变量提升](http://www.cnblogs.com/damonlan/archive/2012/07/01/2553425.html)
[使用Greensock的高级Javascript动画示例和展示-greensock](https://greensock.com/examples-showcases)
[我接触过的前端数据结构与算法](https://juejin.im/post/5958bac35188250d892f5c91)
[使用自动生成器创建页面 -  GitHub Enterprise 2.11文档](https://help.github.com/enterprise/2.11/user/articles/creating-pages-with-the-automatic-generator/)
[全新Chrome Devtool Performance使用指南](https://zhuanlan.zhihu.com/p/29879682)
[页面重绘和回流以及优化 ](http://www.css88.com/archives/4996)
[JS刷题总结](https://zhuanlan.zhihu.com/p/35444353)
[JS中lambda表达式的优缺点和使用场景(转)](https://www.cnblogs.com/ajianbeyourself/p/8859261.html)
[第28篇 js中let和var](http://www.cnblogs.com/OceanHeaven/p/5472181.html)
[android JSON解析之JSONObject与GSON](https://www.cnblogs.com/gzdaijie/p/5189542.html)
[使用控制台 - Chrome 开发工具指南 - 极客学院Wiki](http://wiki.jikexueyuan.com/project/chrome-devtools/using-the-console.html)
[SQL Server 存储过程](https://www.cnblogs.com/hoojo/archive/2011/07/19/2110862.html)
[DECLARE (Transact-SQL)](https://docs.microsoft.com/zh-CN/sql/t-sql/language-elements/declare-local-variable-transact-sql?view=sql-server-2017)
