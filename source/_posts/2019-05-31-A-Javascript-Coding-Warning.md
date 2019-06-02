---
title: A-Javascript-Coding-Warning
date: 2019-05-31 16:24:24
tags:
    - JacaScript
description: '解决 unreachable code after return statement 警告'
categories:
    - Experience
---

# Main Content
![处理前](/assets/img/sharding/err/instanceOf-old.png)
此[commit](https://github.com/SailHe/lost_and_found/commit/4d438b403c6e64a9cdc5899095877a122c18ba15)修复了该潜在bug
## What
大约就是写了这种代码:
```js
return
    1 + 2;
```

## How
应该这么写:
```js
return 1 + 2;
```
![处理后](/assets/img/sharding/err/instanceOf-new.png)

## Why
1. 脚本代码执行以行为单位
2. js代码行末可以不用写';' -> return 可以视为一条单独的语句

---
# Reference
## SEK
NONE

## Links
1. [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Errors/Stmt_after_return?utm_source=mozilla&utm_medium=firefox-console-errors&utm_campaign=default)

## Else
None
