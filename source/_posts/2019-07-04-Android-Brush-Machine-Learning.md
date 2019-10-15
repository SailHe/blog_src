---
title: Android-Brush-Machine-Learning
tags:
  - Android
description: Android折腾记录
categories:
  - 折腾
date: 2019-07-04 22:05:59
---

# 前言

**ROM包**，也叫固件包

[Root (Android) - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/Root_(Android))

- [ ] 刷机
    - 机型太辣鸡(vivo) 据说: 最好刷机的{三星 华为 小米} 国内华为还好，vivo最绝，全网都找不到twrp和包，oppo第二，只是超级难刷而已。
    - 但是没有对应的纯净Rom包, 也没有合适的TWRP, 若自己制作需要搭建编译Android内核的开发环境, 貌似只有Linux才行
    - 于是问题转化为安装Linux系统, 编译Android属于CPU密集的工作需要较高性能, 于是虚拟机估计不行, 那就只有WSL或双系统
    - WSL担心坑太多之前的使用体验不佳不清楚功能是否齐全, 另装一个系统风险又有点大
    - `很久以前我也喜欢折腾这些 直到后来我买了第二台电脑`
    - 关键是现在浏览器环境有些问题(证书过期事件2019-05-01日--5日)
    - 然后被FireFox当时的[证书过期事件](/2019/07/04/FireFox-Customize/#证书过期事件)中断了计划
    - 期间还尝试使用[复制链接的拓展](/2019/07/04/FireFox-Customize/#复制链接的拓展)但其项目由于拓展被下架 编译失败 故直至10月份初才搞定

## 机型
Oppo A53: color os 2.1 android 5.1.1
Vivo Y27

- [Download Vivo Y27 Stock Firmware (flash file)](https://firmwarefile.com/vivo-y27)
- [How to use QPST Flash Tool](https://androidmtk.com/use-qpst-flash-tool)
- [QPST+Flash+Tool+2.7](https://www.google.com/search?ei=cEXUXNvOJMjH5gLE57aACw&q=QPST+Flash+Tool+2.7+教程&oq=QPST+Flash+Tool+2.7+教程&gs_l=psy-ab.3...983353.985565..986130...0.0..0.0.0.......0....1..gws-wiz.6gtLh4LKcfQ)
- [QPST+Flash+Tool+vivo+y27](https://www.google.com/search?client=firefox-b-d&q=QPST+Flash+Tool+vivo+y27)
- [how-to-fix-invalid-imei-meid-change](https://forum.xda-developers.com/android/general/how-to-fix-invalid-imei-meid-change-t3713573)
- [unbricking-qfil-sahara-fail-error-help](https://forum.xda-developers.com/android/help/unbricking-qfil-sahara-fail-error-help-t3823986)

# Recovery
`Android 成熟的系统备份程序`

.\fastboot.exe bbk unlock_vivo
adb reboot bootloader
./fastboot devices
./fastboot.exe flash boot ..\vivo_y27\boot.img
./fastboot.exe flash recovery ..\recovery\RedMiNote4\cofface_nikel_recovery.img
./fastboot.exe reboot

1晚上8%的電(沒有軟件运行的待机)

>V2EX★★2019年7月5日5楼15单元
 关于华为，再说一下让人觉得恶心的地方。
 喜欢折腾 Android 手机的人，应该都知道：华为在去年就以“安全”为由取消提供原厂系统 EMUI 的下载，后来干脆不给手机提供解锁 Bootloader 服务了。(后来很多老外提出抗议，荣耀系列恢复解锁申请服务)
 对于普通用户来说，这两件事没有什么影响，如果你喜欢折腾手机，请不要买华为。

>华为从来就不是什么开放的公司，你的美好幻想只能在梦里出现。
 国内最开放的手机厂商应该是一加，他们鼓励玩家刷机，连 root 甚至刷机都保修，世界上再难找到第二个这样的手机厂商，我现在就用一加的手机。
 当然一加手机也有缺点，比如屏幕，甚至有人吐槽一加的品控。

## Magisk
[[2019.10.11] Magisk v20.0 - Root & Universal Systemless Interface [Android 4.2+]](https://forum.xda-developers.com/apps/magisk/official-magisk-v7-universal-systemless-t3473445)
`原文`[Installation | Magisk](https://topjohnwu.github.io/Magisk/install.html)

### 安装教程

- 机翻润色


    如果您已经安装了Magisk， 强烈建议您直接通过Magisk Manager进行升级 。 以下教程适用于初次使用的用户。
    如果您使用的是运行EMUI 8及更高版本的华为设备，请查看自己的部分。
    如果您使用的是使用Android 9.0启动的Samsung设备（2019年的新设备），请查看其自己的部分。 
    
#### **条件**
    
    如果您计划安装自定义内核，请在安装Magisk 之后刷新zip
    确保删除任何“启动映像mods”，如其他根解决方案。 最简单的方法是从工厂映像恢复启动映像，或重新刷新非预根的自定义ROM 

#### **自定义恢复**

如果您的设备具有自定义恢复支持，最简单的方法是通过自定义恢复（如TWRP）进行安装。

    下载Magisk安装程序zip
    重新启动到自定义恢复
    闪存拉链并重新启动
    检查是否已安装Magisk Manager。 如果由于某种原因未自动安装，请手动安装APK 

#### **启动映像修补**

这是在您的设备上安装Magisk的“酷”方式。 您的设备没有正确的自定义恢复，您的设备正在使用A / B分区方案，并且您不想将恢复和启动映像混合在一起，或者您有其他问题（例如OTA安装 ），您应该使用此方法代替。

要使用此方法，您需要获取库存启动映像的副本，可以通过提取OEM提供的工厂映像或从OTA更新拉链中提取来找到该映像。 如果您自己无法获得一个，互联网上的某个人可能会在某个地方共享它。 获得引导映像副本后，以下说明将指导您完成此过程。

    将启动映像复制到您的设备
    下载并安装最新的Magisk Manager
    按安装→安装→选择并修补文件 ，然后选择库存启动映像文件
    Magisk Manager将Magisk安装到您的启动映像，并将其存储在[Internal Storage]/Download/magisk_patched.img
    将修补的启动映像从设备复制到PC。 如果您无法通过MTP找到它，可以使用ADB提取文件：
    adb pull /sdcard/Download/magisk_patched.img
    将已修补的引导映像刷新到您的设备并重新启动。 如果在大多数设备上使用fastboot，这是命令：
    fastboot flash boot /path/to/magisk_patched.img

#### **恢复中的Magisk**

由于某些设备不再在启动映像中使用ramdisk，因此Magisk别无选择，只能安装在恢复分区中。 对于这些设备，如果需要Magisk，则每次都必须启动恢复 。 由于Magisk和恢复都位于同一个分区中，因此当您选择启动恢复时，实际上最终获得的内容将取决于您按下音量的时间 。

每个OEM都有自己的密钥组合来启动恢复。 例如在三星上它是（Power + Bixby + Volume Up） ，而对于华为则是（Power + Volume Up） 。 只要您按下组合并且设备以启动屏幕振动，引导加载程序就已经选择了它启动的模式，无论是boot ， recovery还是某些OEM特定模式，如download ，快速boot或电子erecovery 。 在启动屏幕之后，释放所有按钮以启动到Magisk，因为默认recovery模式将启动到启用Magisk的系统。 如果您决定启动到实际恢复，请继续按音量调高，直至看到恢复屏幕。

总之，安装Magisk之后：

    （正常上电）→（没有Magisk的系统）
    （OEM恢复键组合）→（启动画面）→（释放所有按钮）→（带Magisk的系统）
    （OEM恢复键组合）→（启动画面）→（保持按下音量）→（实际恢复） 

三星（System-as-root）

如果您的设备未使用Android 9.0或更高版本（2019年之后发布）启动，请按照常规教程进行操作
安装Magisk之前

    安装Magisk会让KNOX旅行
    首次安装Magisk 需要在继续之前备份完整数据，备份
    在按照说明操作之前，您必须解锁引导加载程序
    Magisk将安装到您设备的恢复分区。 请按照以下说明阅读“恢复中的Magisk”部分！
    安装Magisk后，您可以直接在Magisk Manager中升级Magisk而不会出现问题。 目前不支持自定义恢复中的闪烁。 


---


择并修补文件，然后选择AP tar文件。
    Magisk Manager将修补整个固件文件并将输出存储到[Internal Storage]/Download/magisk_patched.tar
    将tar文件复制到PC，然后将设备启动到下载模式。
    在ODIN magisk_patched.tar作为AP
    重要提示：在选项中取消选中“自动重启”！
    Magisk现已成功闪存到您的设备！ 但是，在正确使用设备之前，仍有几个步骤。
    我们现在想启动库存恢复工厂重置我们的设备。
    全数据擦除是强制性的！ 不要跳过此步骤。
    按电源+降低音量以退出下载模式。 屏幕关闭后，立即按Power + Bixby + Volume Up启动恢复分区。 正如上一节所述，由于我们要启动库存恢复，请继续按下音量增大按钮，直到看到库存恢复屏幕 。
    在库存恢复菜单中，使用音量按钮浏览菜单，使用电源按钮选择选项。 选择擦除数据/恢复出厂设置以擦除设备的数据。
    这次，我们终于可以使用Magisk启动系统了。 选择立即重启系统 ，然后立即按Power + Bixby + Volume Up 。 看到引导加载程序警告屏幕后，释放所有按钮，以便它可以引导到系统。
    设备首次启动时会自动重启。 这完全正常并且是通过设计完成的。
    设备启动后，执行常规初始设置。 以下步骤需要互联网连接。
    您将在应用程序抽屉中看到Magisk Manager; 如果没有，请手动安装您在步骤3中下载的APK，然后继续执行下一步。 该应用程序将是一个存根，它将在您打开它时自动升级到完整的Magisk Manager。
    Magisk Manager将要求进行其他设置。 让它完成它的工作，应用程序将自动重启您的设备。
    瞧！ 享受Magisk :) 

#### 附加信息

    Magisk实际上修补了您设备上的3个分区：
        vbmeta ：替换为空的vbmeta镜像以禁用分区验证
        boot ：删除镜像的签名以防止软砖
        recovery ：这是Magisk实际安装的地方 
    永远不要试图恢复提到的3个镜像中的任何一个！ 您可以通过这样做轻松地对设备进行打砖，唯一的出路是在出厂重置后进行完整的ODIN恢复。 只是不要这样做。
    如果要升级设备，请不要使用上述原因刷新库存AP tar文件。 始终在ODIN中闪烁之前预先修补固件。
    如果您不需要修补完整固件，则可以手动创建至少包含 vbmeta.img ， boot.img和recovery.img的tar文件，以便让Magisk Manager以正确的方式修补您的镜像。 

#### 华为

使用麒麟处理器的华为设备采用与大多数常见设备不同的分区方法。 Magisk通常安装在设备的boot分区，但华为设备没有此分区。 根据您的设备运行的EMUI版本，说明会略有不同。
获得股票镜像

华为不发布官方工厂映像，但大多数固件压缩都可以从华为固件数据库下载。 要从zip中的UPDATE.APP中提取镜像，您必须使用华为更新提取器 （仅限Windows！）
EMUI 8

对于EMUI 8设备，您的设备有一个名为ramdisk的分区，这是安装Magisk的地方。

    如果您打算使用自定义恢复，只需按照自定义恢复的说明进行操作即可。
    如果您打算不使用自定义恢复，则必须从固件中提取RAMDISK.img 。 按照上面的启动映像修补说明进行操作，但使用RAMDISK.img文件而不是启动映像。
    要将修补后的映像刷新到设备，请执行以下命令：fastboot命令：
    fastboot flash ramdisk /path/to/magisk_patched.img
    请注意，你正在闪烁到ramdisk ，而不是boot ！ 

#### EMUI9+

对于EMUI 9+设备， ramdisk分区不再存在。 作为解决方法，Magisk将安装到recovery_ramdisk分区。 请按照以下说明阅读“恢复中的Magisk”部分！

注意：正如我在Honor View 10上测试的那样，华为的内核似乎无法在早期启动时捕获按键按键事件，因此长按Volume Up无法在设备上启动恢复。 您的体验可能有所不同

    如果您打算使用自定义恢复，只需按照自定义恢复的说明进行操作即可。
    警告：Magisk将覆盖自定义恢复。
    如果您打算不使用自定义恢复，则必须从固件中提取RECOVERY_RAMDIS.img 。 按照上面的启动映像修补说明进行操作，但使用RECOVERY_RAMDIS.img文件而不是启动映像。
    要将修补后的映像刷新到设备，请执行以下命令：fastboot命令：
    fastboot flash recovery_ramdisk /path/to/magisk_patched.img
    请注意，您正在闪烁到recovery_ramdisk ，而不是boot ！ 


#### 解锁Bootloader

通常情况下，我不会提供相关说明，但由于以前的三星设备发生了很大的变化，并且有一些细节可能不为人所知，我认为这会有所帮助。

    允许在Developer选项中解锁引导加载程序→OEM解锁
    关闭设备电源。 按Bixby + Volume Down并将设备插入PC以启动进入下载模式
    长按音量可解锁引导加载程序。 这将擦除您的数据并自动重启。 

就在您认为引导加载程序已解锁时，出乎意料的惊喜， 实际上并非如此！ 三星在系统中引入了VaultKeeper ，这意味着在VaultKeeper明确允许之前，引导加载程序将拒绝任何非官方分区。

    完成初始设置。 跳过所有步骤，因为稍后在我们安装Magisk时将再次擦除数据。 在设置中将设备连接到互联网！
    启用开发人员选项，并确认OEM解锁选项存在且显示为灰色！ VaultKeeper服务在确认用户启用了OEM解锁选项后将释放引导加载程序。 此步骤只是确保服务获取正确的信息，并仔细检查我们的设备是否处于正确状态
    您的引导加载程序现在可以在下载模式下接受非官方镜像。 

#### 说明

    下载设备的固件。
    解压缩固件并将AP tar文件复制到您的设备。 它通常命名为AP_[device_model_sw_ver].tar.md5
    安装最新的Magisk Manager
    在Magisk Manager中： 安装→安装→选


## 未知设备
[Android刷机手册（小白向）--① 卡刷和线刷](https://baolong24.github.io/2019/06/10/android/)
按住电源键和音量下(估计与进入fastboot为同一方式 实在不行就所有键一起按)大约40s后会出现9008的com端口
全称Qualcomm HS-USB QDLoader 9008(COM10)
详情如图所示

`SK: Qualcomm USB Driver V1.0.exe 安装教程`
[ 高通刷机工具下载 ](http://www.shuajibang.net/tool/detail/6192)
[高通驱动安装教程](https://blog.csdn.net/qq_43653944/article/details/86702169)
`SK: Qualcomm USB Driver V1.0.exe 9008`

[Comparison_of_online_backup_services](https://en.wikipedia.org/wiki/Comparison_of_online_backup_services)

[KB4100347：Intel 微码更新](https://support.microsoft.com/zh-cn/help/4100347/intel-microcode-updates-for-windows-10-version-1803-and-windows-server)


 摩托罗拉Moto-E-XT1022 
 您需要适当的Windows驱动程序。 Windows XP和Windows 7/8/10之间存在体系结构差异。 
 在Windows XP上，安装和过程非常简单明了（我在Windows 2003上也成功进行了测试），但是在Windows 7或8或10上运行时，事实证明这是一个很大的挑战，尽管您可以随意安装。 
 越来越多的人报告在Windows 7/8/10上尝试取消常规过程时遇到的问题，有些运气比另一些好。 有些人的运气为零。 
 话虽如此，如果您可以使用Windows XP计算机，我强烈建议您使用它。 
 如果您别无选择，只能使用Windows 7、8或10计算机，并且有问题，请在我的XDA DevDB项目线程中共享它们，并阅读其他人的经验。


# 虚拟机刷机

由于涉及东西太多
试了几次没成

`SK: 	ERROR: function: sahara_rx_data: 237 site: developer.qualcomm.com`

`为何操作理论上都正确但就是不行`

>我的问题已经解决了。 之后我从ubuntu 10.04 i386更改为ubuntu 10.04 AMD64并安装了所有更新。 
>我的USB设备有效。
>我认为这个问题**与操作系统更相关**，因为我使用相同版本的虚拟机（但是amd64比i386）并且现在可以使用了。

## 虚拟方式对比

**Hyper-V**最初是与Windows Server 2008一起发布的, 后者于2008年2月4日发布，并于2008年2月27日全面上市

[Windows 10 上的 Hyper-V 简介 | Microsoft Docs](https://docs.microsoft.com/zh-cn/virtualization/hyper-v-on-windows/about/)

Microsoft Hyper-V ，代号为Viridian，以前称为Windows Server Virtualization ，是一个原生的 hypervisor ; 它可以在运行Windows的 x86-64系统上创建虚拟机 。 
从Windows 8开始，Hyper-V取代了Windows Virtual PC作为Windows NT客户端版本的硬件虚拟化组件。 可以将运行Hyper-V的服务器计算机配置为将单个虚拟机公开给一个或多个网络。
[WSL](https://zh.wikipedia.org/wiki/适用于_Linux_的_Windows_子系统)
微软明确指出WSL面向应用程序的开发者，而不是面向桌面环境或生产服务器，建议使用虚拟机（Hyper-V或Kubernetes）和Azure来实现这些目的。


对于ViutualBox
虚拟硬盘存在固态硬盘的情况下
开启debian命令行也就500M不到的RAM
开启Win10-dev就1.9G RAM
对于Hyper-v(虚拟硬盘存在固态硬盘的情况下)貌似内存分配的方式有所不同, 总会在某个时刻到达2G, 而且就Win10-dev而言速度并不比VBox快(两者体验都不流畅)


## 尝试

一共在虚拟机上尝试了
2次win10安装(Vbox和hyper-v各一次)
2次debain安装(Vbox和hyper-v各一次)
hypwe-v: 1+1(最后装引导时识别出了现有的Win10 vista 但失败 具体忘记了)+1+1(虚拟debian覆盖了Win10 而且与之前的覆盖不同 也许是移动了虚拟硬盘位置的缘故 无法还原 故作罢) = 4
vbox: 1+1(虚拟双系统)
还尝试了一次命令行安装, 这种安装方式没有中文

### 安装图形化界面

一共尝试了5趟(没退出安装界面的情况下算作一趟)
**第一趟** 由于忘记切换安装镜像, 虽然成功安装, 但安装的是网络安装的镜像, 因此只有命令行界面, 此次安装是最顺利和最流畅的一次
**第二趟** 第一次貌似由于磁盘容量不足而错误 第二次没有成功检测出引导导致原系统被覆盖
**第三趟** 共安装了3次
**第四趟** 安装了至少4次
**第五趟** 新加了一个未分配的分区安装了1次 全没有检测出来, 但是这所有情况只要最后没有安装引导都可以回到之前的系统
**第六趟** 将原有的俩主分区删除并合并到未分配分区, 即: 除了Win10所在的分区外保有一个空闲分区
(那俩主分区并非空闲分区 应该是之前安装Debian-CMD时的遗留物)

最后我整理了一遍快照, 又试了一遍, 得出结论确实如此: 
1. 安装前保证存在1个空闲分区(仍不确定能否有多个 应该行)
2. 然后选择离线安装的镜像
   - 取消连接并忽略联网
   - 安装软件的时候注意选择图形化界面
3. 最后确认最后安装引导的时候是否检测出了原有系统
    - 如果检测出来, 直接安装到主分区即可(默认总是第一个选项 并非默认选项)
    - 如果没有检测出来选择取消然后中止安装即可保留原有系统

如果是网络安装版 最好断网安装, 否则下载会下载很久, 关闭网络后配置网络那里理应失败, 不要手动配置, 跳过即可
最后的引导若提示识别出了原有的Win系统则直接将引导放到默认给出的那里即可, 然后自动重启进入系统时如果成功的话会出现三个选项, 其中一个是原有的Win10
