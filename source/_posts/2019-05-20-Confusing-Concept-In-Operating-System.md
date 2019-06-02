---
layout: post
title:  "Confusing-Concept-In-Operating-System"
image: ''
date:   2019-05-20 21:11:31
tags:
    - Docs
description: '操作系统中的一些易混淆概念'
categories:
    - Operating-System
---


# 基本概念简介:
## 控制台: 
>即[命令行界面] (英语：command-line interface，缩写：CLI)
 也有人称之为[字符用户界面] (character user interface, CUI)

        是在[图形用户界面]得到普及之前使用最为广泛的用户界面，
        通常不支持鼠标，用户通过键盘输入指令，计算机接收到指令后，予以执行。
        用于提供丰富的控制与自动化的系统管理能力

    例如 Linux系统的Bash或是Windows系统的Windows PowerShell。
	
## [DOS系统](https://zh.wikipedia.org/wiki/DOS): 
> 磁盘操作系统(Disk Operating System, DOS): 是个人计算机上的一类操作系统。
    
    透过批处理文件（扩展名为.BAT）提供界面脚本的功能。
    所有的DOS均使用命令行界面。运行程序的方法是在命令行中键入程序的名称。
    DOS系统包含一些公用程序，也提供了一些不是以程序方式存在的命令（常称为内部命令）

## 壳层(Shell)

[命令提示字元-Wiki](https://zh.wikipedia.org/wiki/命令提示字元)
[CMD官方文档](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/cmd)
[Powershell-Wiki](https://zh.wikipedia.org/wiki/Windows_PowerShell)
[Powershell官方文档](https://docs.microsoft.com/en-us/powershell/scripting/learn/understanding-important-powershell-concepts?view=powershell-6)
[Win-commands官方文档](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)


>指"为用户提供用户界面"的软件，通常指的是命令行界面的解析器。
    一般来说，这个词是指操作系统中提供访问内核所提供之服务的程序。
    
>Shell也用于泛指所有为用户提供操作界面的程序，也就是程序和用户交互的接口。
    因此与之相对的是内核（英语：Kernel），内核不提供和用户的交互功能。

>不过这个词也拿来指应用软件，或是任何在特定组件外围的软件，例如浏览器或电子邮件软件是HTML排版引擎的shell。
 Shell这个词是来自于操作系统（内核）与用户界面的外层界面。

    管道: 
	
		管道(|), 是Shell的重要概念, EG: 将dir命令的输出定向到find命令 dir c:\ /s /b | find "CPU"
		dir | findstr "tmp" 这使得findstr可以对文件夹信息进行搜索
		命令大全(通过命名方式可知 这些命令, 例如netstat应该是一些程序或是脚本, 不是Powershell的语言本身)

	通常分类:

		命令行壳层: 提供命令行界面(CLI 英文 Command Line Interface for batch scripting);
		
			Windows操作系统->Windows 95 / 98下的command.com、Windows NT内核下的cmd.exe以及PowerShell
			
				命令解释程序(command interpreter) Cmd.exe
                    命令行(Command-Line)
                    脚本拓展名: *.cmd
					
				Powershell
				
					不仅仅是Shell, 由于以.NET Framework技术为基础, 可以视作是一门脚本语言
					脚本拓展名: *.ps1
					
		图形壳层: 提供图形用户界面(GUI);
		
			Windows操作系统->explorer.exe(俗称文件浏览器)
			

## 终端(terminal)
> 是一台计算机或者计算机系统，用来让用户输入数据，及显示其计算结果的机器。
> Virtual-Terminal
> Hardware-Terminal

---

## 常见cmd命令
```cmd
	:: 注释符(PS: 命令中的字母一般无大小写之分但符号必须一定为英文下打的)
	dir :: 显示当前目录下文件(Alias: ls 但在CMD下不可用)
	cd\... :: 回到驱动器目录?
	d: :: 切换驱动器盘符(并不切换路径), Powershell的cd能够直接切换盘符, CMD中切换盘符和切换目录是两码事
	cd h:\java ::进入H盘下的java目录
	at 12:00 filePath :: 表示在12:00打开filePath对应的文件(现已弃用)
	start ::(当前命令提示符窗口中打开新的命令提示符窗口)
```
    显示活动的TCP连接，计算机正在侦听的端口，以太网统计信息，IP路由表，IPv4统计信息(用于IP，ICMP，TCP和UDP协议)和IPv6统计信息(用于IPv6，ICMPv6，TCP over IPv6)和IPv6 over IPv6协议:
```cmd
    netstat -aon|findstr "端口" :: 可以不用引号 指定端口没有被占用则没有返回
    tasklist|findstr "PID" :: 也可以在任务管理器的详情信息根据PID查询
    taskkill /f /t /im 占用进程名.exe :: 杀死服务以释放被占用的端口
```

**以下源于中文网络, 或不可靠, 最好参考MS官方文档, 若没有中文版本, 实机上的帮助文档可能有中文**
```cmd
command /? :: 输出command命令的帮助文档
```
> P1
　　winver---------检查Windows版本 
　　wmimgmt.msc----打开windows管理体系结构(WMI) 
　　wupdmgr--------windows更新程序 
　　wscript--------windows脚本宿主设置 
　　write----------写字板 
　　winmsd---------系统信息 
　　wiaacmgr-------扫描仪和照相机向导 
　　winchat--------XP自带局域网聊天
> P2
　　mem.exe--------显示内存使用情况 
　　Msconfig.exe---系统配置实用程序 
　　mplayer2-------简易widnows media player 
　　mspaint--------画图板 
　　mstsc----------远程桌面连接 
　　mplayer2-------媒体播放机 
　　magnify--------放大镜实用程序 
　　mmc------------打开控制台 
　　mobsync--------同步命令
> P3
　　dxdiag---------检查DirectX信息 
　　drwtsn32------ 系统医生 
　　devmgmt.msc--- 设备管理器 
　　dfrg.msc-------磁盘碎片整理程序 
　　diskmgmt.msc---磁盘管理实用程序 
　　dcomcnfg-------打开系统组件服务 
　　ddeshare-------打开DDE共享设置 
　　dvdplay--------DVD播放器
> P4
　　net stop messenger-----停止信使服务 
　　net start messenger----开始信使服务 
　　notepad--------打开记事本 
　　nslookup-------网络管理的工具向导 
　　ntbackup-------系统备份和还原 
　　narrator-------屏幕“讲述人” 
　　ntmsmgr.msc----移动存储管理器 
　　ntmsoprq.msc---移动存储管理员操作请求 
　　netstat -an----(TC)命令检查接口
> P5
　　syncapp--------创建一个公文包 
　　sysedit--------系统配置编辑器 
　　sigverif-------文件签名验证程序 
　　sndrec32-------录音机 
　　shrpubw--------创建共享文件夹 
　　secpol.msc-----本地安全策略 
　　syskey---------系统加密，一旦加密就不能解开，保护windows xp系统的双重密码 
　　services.msc---本地服务设置 
　　Sndvol32-------音量控制程序 
　　sfc.exe--------系统文件检查器 
　　sfc /scannow---windows文件保护
> P6
　　tsshutdn-------60秒倒计时关机命令 
　　tourstart------xp简介（安装完成后出现的漫游xp程序） 
　　taskmgr--------任务管理器 
　　eventvwr-------事件查看器 
　　eudcedit-------造字程序 
　　explorer-------打开资源管理器 
　　packager-------对象包装程序 
　　perfmon.msc----计算机性能监测程序 
　　progman--------程序管理器 
　　regedit.exe----注册表 
　　rsop.msc-------组策略结果集 
　　regedt32-------注册表编辑器 
　　rononce -p ----15秒关机 
　　regsvr32 /u *.dll----停止dll文件运行 
　　regsvr32 /u zipfldr.dll------取消ZIP支持
> P7
　　cmd.exe--------CMD命令提示符 
　　chkdsk.exe-----Chkdsk磁盘检查 
　　certmgr.msc----证书管理实用程序 
　　calc-----------启动计算器 
　　charmap--------启动字符映射表 
　　cliconfg-------SQL SERVER 客户端网络实用程序 
　　Clipbrd--------剪贴板查看器 
　　conf-----------启动netmeeting 
　　compmgmt.msc---计算机管理 
　　cleanmgr-------垃圾整理 
　　ciadv.msc------索引服务程序 
　　osk------------打开屏幕键盘 
　　odbcad32-------ODBC数据源管理器 
　　oobe/msoobe /a----检查XP是否激活 
　　lusrmgr.msc----本机用户和组 
　　logoff---------注销命令 
　　iexpress-------木马捆绑工具，系统自带 
　　Nslookup-------IP地址侦测器 
　　fsmgmt.msc-----共享文件夹管理器 
　　utilman--------辅助工具管理器 
　　gpedit.msc-----组策略
