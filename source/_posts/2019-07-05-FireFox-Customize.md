---
title: FireFox-Customize
tags:
  - 折腾
description: 自定义FireFox
categories:
  - Induction
date: 2019-07-05 22:10:32
---

# Tips
- FireFox使用Google服务(比如reCAPIcHA验证服务)老出现奇怪的问题(就是打不开...更换ip也不行), 可以尝试更新hosts+刷新DNS缓存
- `SK: unreachable code after return statement`[详细了解](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Errors/Stmt_after_return?utm_source=mozilla&utm_medium=firefox-console-errors&utm_campaign=default)
- GoogleTranslate首次翻译会进入带有翻译面板的: https://translate.google.com/
- 在上述翻译的页面点击会进入不带翻译面板的: https://translate.googleusercontent.com
- 但难以直接进入后一个网站: 需要某种东西进行验证(可能是被翻译页面的Hash, 或者token什么的)


# 常见需求&解决方案

解决方案
  1. [已存在的功能](/2019/07/05/FireFox-Customize/#Tips)
  2. 附加组件
  3. 脚本

- `脚本`从Google翻译界面获取原文链接

啊...非常脑残的实现, 效果不咋地:
```js
// ==UserScript==
// @name Google翻译(上下文)将原链接输出至控制台
// @namespace Violentmonkey Scripts
// @match https://translate.googleusercontent.com/translate_c
// @require		https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js
// @grant none
// ==/UserScript==

(function() {
  'use strict';
  // window.location.host
  let current_url = window.location.href.substr(113);
  current_url = current_url.substr(0, current_url.indexOf("&"));
  // console.copy(current_url);
  console.clear();
  console.log("已清空");
  console.log(current_url);
})();

```
- `脚本`将google搜索界面的统计链接换为直链: 已有类似实现->搜索
- `附加组件`站内搜索FireFox插件(或者基于支持站内搜索语法的搜索引擎)
  1. 可使用[GlitterDrag](https://github.com/SailHe/GlitterDrag)实现
- `脚本`匹配URL

1. 正则表达式, 原理之类的
[js 正则匹配 域名【host】](https://www.cnblogs.com/cench/p/6718466.html)
`SK: JS 判断是否合法URL`[求一个验证url合法性的正则，网上找了很多都有漏洞](https://segmentfault.com/q/1010000015105890)
>`SK: 使用异常来做判断`[用Exception异常还是if判断](https://tech.msla.top/2017/09/11/用exception异常还是if判断/)
 java规范的定义是说异常不要参与控制流程，你不能把异常作为一种正常的控制流程作为程序的一部分，这样是不对的.
[js 正则匹配 域名【host】 - cench - 博客园](https://www.cnblogs.com/cench/p/6718466.html)
```js
/^http(s)?:\/\/(.*?)\//.exec(location.href)
location.href.split(/^http(s)?:\/\/(.*?)\//)
```
1. 代码
```js
const checkURL = (url) => {
	var str = url;
	//判断URL地址的正则表达式为:http(s)?://([\w-]+\.)+[\w-]+(/[\w- ./?%&=]*)?
	//下面的代码中应用了转义字符"\"输出一个字符"/"
	var Expression = /http(s)?:\/\/([\w-]+\.)+[\w-]+(\/[\w- .\/?%&=]*)?/;
	var objExp = new RegExp(Expression);
	if(objExp.test(str) == true){
		return true;
	}else{
		return false;
	}
}
// checkURL('index');  // false
// checkURL('http://www.baidu.com');  // true
```

- 文本管理
  1. [0x6b/copy-selection-as-markdown: Firefox add-on to copy selection as Markdown](https://github.com/0x6b/copy-selection-as-markdown)
- 标签页管理
  1. [better-onetab](https://github.com/cnwangjie/better-onetab)

# 其他
## 安全
- FireFox 提示此网站中某些内容(例如图像)不安全时 尝试屏蔽http传输的内容
- 对于http的网站 如果被重定向至 `貌似现在被卖了...`[139](https://www.139.site) 则说明被劫持了 此时可以尝试https(一般可以访问 但可能存在内容与http不对应的情况), 或是尝试类似TOR的加密线路
- 简单来说有的网站http方式甚至是无法访问的(流氓式恶意重定向)
- 有的网站会在某个特定的时间段内对原有http的网站进行重定向Https, 现象大概就是网址变化+书签标记变化(如果存了书签的话)

## 证书过期事件
`附加组件全部失效`
about:config
signatures.required
[Mozilla曝出大乌龙 证书过期导致全球Firefox用户无法使用扩展](http://www.dbsec.cn/zx/20190505-5.html)
可以避免附加组件的签名验证
[Solidot | 如何修复 Firefox 的扩展签名过期](https://www.solidot.org/story?sid=60486)
[Solidot | 因中级证书过期 Firefox 扩展停止工作](https://www.solidot.org/story?sid=60476)
[Intermediate signing certificate expiry causes All Firefox add-ons to be disabled or fail to install](https://techdows.com/2019/05/firefox-add-ons-disabled-and-fail-to-install-due-to-certificate-issue.html)
[Add-ons disabled or failing to install in Firefox | Mozilla Add-ons Blog](https://blog.mozilla.org/addons/2019/05/04/update-regarding-add-ons-in-firefox/)
[1549017 - All extensions disabled due to expiration of intermediate signing cert (Workaround on standard builds)](https://bugzilla.mozilla.org/show_bug.cgi?id=1549017)
