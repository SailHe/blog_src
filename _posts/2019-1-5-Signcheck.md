---
layout: post
title:  "Win 使用 sigcheck"
image: ''
date:   2019-01-08 20:59:25
tags:
- sigcheck 计算机安全 哈希验证 SHA
description: 'template for blog'
categories:
- Learning
---

## Google Keywords

win sigcheck

### sigcheck 下载链接

1. <a href="https://docs.microsoft.com/en-us/sysinternals/downloads/sigcheck" target="_blank">微软官网</a>

PS: 
1. 将一个文件打包后上传可能没有报毒 但解压后一些文件单独上传则有可能
2. 使用https://www.virustotal.com/进行检测并返回结果 详细文档参考: https://docs.microsoft.com/en-us/sysinternals/downloads/sigcheck
sigcheck.exe -v
sigcheck.exe -v -s -u   表示使用vt对当前目录进行子目录递归检测 并只显示没有签名 unknown by VirusTotal or have non-zero detection(未知或是有报毒的文件, 实际上貌似只显示报毒的 未知的并没有显示) PPS 如果没有加-v, -u只会显示没有签名的文件
这些命令不支持中文路径 或者中文文件名 但是单个上传可以
Unknown可能指没有上传过(自己上传一遍即可); ????可能指鉴定失败(重来一次即可)
事实证明一些软件被报告为恶意 只能说是存在漏洞 并不一定作者就是恶意的(比如说自己写的软件...)

###数字签名
https://baike.baidu.com/item/%E6%95%B0%E5%AD%97%E7%AD%BE%E5%90%8D

###杀软排名
https://www.av-test.org/en/antivirus/home-windows/windows-10/october-2016/

2019-1-8 20:59

---


可以使用[pyWinContext](https://github.com/VodBox/pyWinContext)进行快捷的验证, 之前也用过FileMenuTools,功能更齐全一些, 不过其实没啥必要, 仅仅是添加上下文的话用这款自由软件很方便

最后一次编辑时间: 2019-3-17
