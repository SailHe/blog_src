---
title: Raspberrypi-4
tags:
  - 折腾
description: 树莓派4 raspberrypi4 购买-安装-使用 记录
categories:
  - 树莓派
  - raspberrypi
date: 2019-10-24 23:19:20
---

# 购买
## 选择-Waht
[树莓派版本 - 冠军 - 博客园](https://www.cnblogs.com/haogj/p/4621926.html)
[树莓派|树莓派使用入门：你应该选择哪种树莓派？](https://linux.cn/article-10611-1.html)

## Why
[树莓派基础 - linux中国网wiki](http://wiki.linuxchina.net/index.php?title=%E6%A0%91%E8%8E%93%E6%B4%BE%E5%9F%BA%E7%A1%80#.E6.AD.A3.E7.A1.AE.E5.85.B3.E6.9C.BA)

[树莓派3上手体验_什么值得买](https://post.smzdm.com/p/432173/)
[树莓派 篇一：树莓派3B+，超简单的开箱和购买心得_什么值得买](https://post.smzdm.com/p/a3gzm39d/)

## How
树莓派官网
[Teach, Learn, and Make with Raspberry Pi – Raspberry Pi](https://www.raspberrypi.org/)
[树莓派|树莓派使用入门：如何购买一个树莓派](https://linux.cn/article-10615-1.html)

# 安装系统
## 下载
[FrontPage - Raspbian](https://www.raspbian.org/)
[Download Raspbian for Raspberry Pi](https://www.raspberrypi.org/downloads/raspbian/)

## 安装
`SK: rufus 树莓派 site:github.io`[初入树莓派1安装系统+进入SSH | 默](https://jasper-1024.github.io/2016/06/21/%E5%88%9D%E5%85%A5%E6%A0%91%E8%8E%93%E6%B4%BE1----%E5%AE%89%E8%A3%85%E7%B3%BB%E7%BB%9F+%E8%BF%9B%E5%85%A5SSH/)
`其实直接使用pwershell登录ssh就行了`

### 坑
1. 有数据的TF卡需要格式化, 不应直接写系统镜像, 否则制作完成的镜像可能是有问题的, 比如本人首次的TF卡没有出现BOOT分区

# 使用
[给“树莓派4”加了个风扇，温度直降20度！-电子发烧友网](http://www.elecfans.com/d/998325.html)
[树莓派电源及供电不足问题，及注意事项](http://www.raspigeek.com/index.php?c=read&id=98&page=1)

[树莓派 重启关机命令 | 足迹](http://www.airmn.com/blog/?p=564)

## SSH
`SK: 树莓派 配置 wifi`
[无屏幕和键盘配置树莓派WiFi和SSH | 树莓派实验室](http://shumeipai.nxez.com/2017/09/13/raspberry-pi-network-configuration-before-boot.html)
[树莓派3 启用内置无线网卡连接wifi热点 - 路过未来 - OSCHINA](https://my.oschina.net/TimeCarving/blog/1811631)

`静态IP?`[树莓派 第一次 SSH 启动连接 - raoqin的专栏 - CSDN博客](https://blog.csdn.net/raoqin/article/details/82381296)
> 在cmdline.txt的最后，加上 ip=192.168.1.99 (这个就是树莓派的默认IP)

`SK: 树莓派 4B wifi site:github.io`
[让树莓派运行起来 | Yann's blog](https://yann0917.github.io/2019/08/29/%E8%AE%A9%E6%A0%91%E8%8E%93%E6%B4%BE%E8%BF%90%E8%A1%8C%E8%B5%B7%E6%9D%A5/)
唯一坑到我的是: 
> key_mgmt 为WiFi加密方式，NONE 表示没有密码，WPA-PSK 表示使用**WPA/WPA2**加密；
WPA和WPA2是一样的, 都是`WPA-PSK`不用`WPA2-PSK` 否则无法连接上wifi, 甚至不能软关机...只能拔电源 而且写入的wifi以及ssh配置文件也会被自动删除

[树莓派 3B+ 连接 WPA2 企业级加密的 WIFI | StarryLand](https://rollingstarky.github.io/2018/10/16/raspberry-pi-wifi-wpa2-eap/)

## 说明书
LED指示灯
[R-Pi Troubleshooting - eLinux.org](https://elinux.org/R-Pi_Troubleshooting#Normal_LED_status)

[树莓派指示灯 - 素人派的个人页面 - OSCHINA](https://my.oschina.net/surenpi/blog/891512)
>红灯亮，表示电源已经OK。绿灯无规则的闪烁，表示SD正在被读写。绿灯有规律的闪烁，表示SD没有插好或者是无效的SD卡，也许还可能是无法进入系统。


# 综合

[用 Node.js 玩转树莓派 —— 入门篇 - 十年踪迹的博客](https://www.h5jun.com/post/raspberry-pi.html)
[树莓派从入门到吃土（一） - 简书](https://www.jianshu.com/p/8a5a8ec4fd6b)

[玩转 Raspberry Pi 4 | Bit by bit](https://uinika.github.io/embedded/RaspberryPi.html)
[树莓派4B 玩转指南 | 趙大寳](https://fuhailin.github.io/Raspberry-pi-4/)
```bash
cat /sys/class/thermal/thermal_zone0/temp # 返回值除以1000极为当前CPU温度
```

[第2讲：树莓派新手无痛开机指南【子豪兄的树莓派零基础教程】_哔哩哔哩 (゜-゜)つロ 干杯~-bilibili](https://www.bilibili.com/video/av47603695/?spm_id_from=333.788.videocard.2)
