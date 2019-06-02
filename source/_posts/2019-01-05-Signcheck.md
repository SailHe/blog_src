---
layout: post
title:  "sigcheck"
image: ''
date:   2019-01-08 20:59:25
tags:
    - 程序
    - 计算机安全
    - SHA
    - 哈希验证
description: 'Win 使用 sigcheck'
categories:
    - Evaluation
---

---
# Main Content
## What
检测恶意的可执行程序以及快捷Hash验证

## How
1. 使用[virustotal](https://www.virustotal.com/)进行检测并返回结果, [详细文档参考](https://docs.microsoft.com/en-us/sysinternals/downloads/sigcheck)
``` powershell
./sigcheck.exe -v
```
2. 使用vt对当前目录进行子目录递归检测 并只显示没有签名
> - 官方描述: "unknown by VirusTotal or have non-zero detection"  未知或是有报毒的文件, 实际上只显示了报毒的 未知的并未显示
> - PS 若未使用 -v参数 -u只会显示没有签名的文件
``` powershell
./sigcheck.exe -v -s -u
```

### 注意事项
1. 将一个文件打包后上传可能没有报毒 但解压后一些文件单独上传则有可能
2. 这些命令不支持中文路径, 或者中文文件名, 但是单个上传可以
3. Unknown 一般情况是指没有上传过的文件自己上传一遍即可; 也可能指鉴定失败(重来一次即可)
4. 事实证明一些软件被报告为恶意 只能说是存在漏洞 并不一定作者就是恶意的(比如说自己写的软件...)


## Why
1. 方便
2. 安全


---
# Reference
## SEK
1. win sigcheck

## Links
1. [数字签名](https://baike.baidu.com/item/数字签名)
2. [杀毒软件排名](https://www.av-test.org/en/antivirus/home-windows/windows-10/october-2016/)

## Else
1. 可以结合右键菜单使用
2. 推荐: 专有软件FileMenuTools功能很齐全, 但付费且专有(可试用), 何况没啥必要, 就添加上下文而言用这款自由软件[pyWinContext](https://github.com/VodBox/pyWinContext)很方便
3. Edit 2019-03-17
4. Edit 2019-05-18
