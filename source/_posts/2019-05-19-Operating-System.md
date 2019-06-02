---
title: Operating-System
description: 归纳整理操作系统相关的知识与文档
date: 2019-05-19 22:06:09
tags:
    - Operating-System
    - ESR
categories:
    - Induction
---

>[进程](https://zh.wikipedia.org/wiki/行程)（英语：process），是指计算机中已运行的程序。
>进程为曾经是分时系统的基本运作单位。
>在面向进程设计的系统（如早期的UNIX，Linux 2.4及更早的版本）中，进程是程序的基本执行实体；
>**在面向线程设计的系统（如当代多数操作系统、Linux 2.6及更新的版本）中，进程本身不是基本运行单位，而是线程的容器。**
>**程序**本身只是指令、数据及其组织形式的描述，**进程**才是程序（那些指令和数据）的真正运行实例。
>若干进程有可能与同一个程序相关系，且每个进程皆可以同步（循序）或异步（平行）的方式独立运行。
>现代计算机系统可在同一段时间内以进程的形式将多个程序加载到存储器中，并借由时间共享（或称时分复用），以在一个处理器上表现出同时（平行性）运行的感觉。
>同样的，使用**多线程**技术（多线程即每一个线程都代表一个进程内的一个独立执行上下文）的操作系统或计算机体系结构，同样程序的平行线程，可在多CPU主机或网络上真正同时运行（在不>同的CPU上）。

>[线程](https://zh.wikipedia.org/wiki/线程)（英语：thread）是操作系统能够进行运算调度的最小单位。它被包含在进程之中，是进程中的实际运作单位。
>**一条线程**指的是进程中一个单一顺序的控制流，一个进程中可以**并发**多个线程，每条线程并行执行不同的任务。
>在Unix System V及SunOS中也被称为轻量进程（lightweight processes），但轻量进程更多指内核线程（kernel thread），而把用户线程（user thread）称为线程。
>线程是独立调度和分派的基本单位。线程可以为操作系统内核调度的内核线程，如Win32线程；
>由用户进程自行调度的用户线程，如Linux平台的POSIX Thread；或者由内核与用户进程，如Windows 7的线程，进行混合调度。
>同一进程中的多条线程将共享该进程中的全部系统资源，如虚拟地址空间，文件描述符和信号处理等等。
>但同一进程中的多个线程有各自的调用栈（call stack），自己的寄存器环境（register context），自己的线程本地存储（thread-local storage）。


区分

- 程序: 指令、数据及其组织形式的描述。
- 进程: 是程序的运行实例。
![Hexo blog 服务启动后创建的进程](/assets/opsystme/blog本地运行时的进程.png)
- 线程: 是进程中的实际运作单位。
![正在运行的某程序的线程](/assets/opsystme/程序运行时的线程.png)
- **并发**: 同一个**时间段**存在多个正在运行的线程，且都在同一个处理机上运行，但任一个时刻点上只有一个线程在处理机上运行。
- **并行**: 同一个**时刻**存在多个正在运行的进程。

一个进程可以有很多线程，每条线程并行执行不同的任务。


>**并发**: 当有多个线程在操作时,如果系统只有一个CPU,则它根本不可能真正同时进行一个以上的线程，它只能把CPU运行时间划分成若干个时间段,再将时间 段分配给各个线程执行，在一个时间段>的线程代码运行时，其它线程处于挂起状。.这种方式我们称之为并发(Concurrent)。
>**并行**：当系统有一个以上CPU时,则线程的操作有可能非并发。当一个CPU执行一个线程时，另一个CPU可以执行另一个线程，两个线程互不抢占CPU资源，可以同时进行，这种方式我们称之为>并行(Parallel)。
>区别：并发和并行是即相似又有区别的两个概念，并行是指两个或者多个事件在同一时刻发生；而并发是指两个或多个事件在同一时间间隔内发生。
>在多道程序环境下，并发性是指在一段时间内宏观上有多个程序在同时运行，但在单处理机系统中，每一时刻却仅能有一道程序执行，故微观上这些程序只能是分时地交替执行。
>倘若在计算机系统中有多个处理机，则这些可以并发执行的程序便可被分配到多个处理机上，实现并行执行，即利用每个处理机来处理一个可并发执行的程序，这样，多个程序便可以同时执行。
>[参考](http://term.ccf.org.cn/index.php/并发)

![操作系统基本概念-概览](/assets/opsystme/操作系统基本概念-概览.png)

![进程](/assets/opsystme/进程.png)

![CPU](/assets/opsystme/CPU.png)


---

# shell 和 bash 的区别
[简书参考](https://www.jianshu.com/p/a702a01db5c7)
shell用于将命令翻译成计算机语言，也就是1和0,可以简单的将shell理解为命令行，与之相关的还有shell脚本，就是shell能识别的一连串命令行
bash是shell的一种.
  例如
    Bourne shell(sh); Linux中默认的shell就是Bourne-Again shell(简称bash)
    伯克利分校比尔▪乔伊写的C Shell(csh)，因为类似C语言，故此得名。

# 关于如何使用win子系统安装Linux 以及zsh
[简书参考](https://www.jianshu.com/p/bc38ed12da1d)

zsh: 史称『终极 Shell』, 但配置复杂
--安装zsh 并更改默认shell
[简书参考](https://www.jianshu.com/p/fe244b1c7737)
```bash
sudo apt-get install zsh -y
chsh -s $(which zsh)
```
重启

--oh-my-zsh: zsh的配置项目
[Github参考](https://github.com/robbyrussell/oh-my-zsh)
```bash
git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
cp ~/.zshrc ~/.zshrc.orig # 若存在.zshrc则备份
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc # 创建模板.zshrc
chsh -s /bin/zsh
```


# Ubuntu cmd
Windows：先分区，再格式化。
Linux：一切皆文件。
挂载：将分区和目录绑定在一起。

pwd：打印当前工作目录。
mkdir：创建文件夹。
ls：列出所有子目录以及文件夹。
cd：改变当前工作目录。
tab快捷键：补全目录或者命令。
gedit ARM.c：新建ARM.c文件。
gedit spl.c &：一边编辑文件，一边编译文件，不占用终端，文件在后台运行。
rm：删除文件。
rmdir：删除目录。
rm -rf hsp/: 强制删除文件目录以及下面包含的文件，强制递归删除。
mv main.c test.c: 文件重命名：(移动文件)
cp main.c hsp/main.c: 文件复制。
ps -aux：显示系统正在运行的程序。
pstree：树形显示系统中运行的程序。

kill -9  -3747：杀掉父进程。
shutdown -h now：立即关机
sudo shutdown -h now：切换到root用户再关机。
sudo root：重启。

sudo mv former_name new_name: 修改文件名
sudo mv former_name/ new_name/: 修改文件夹名


# Docker in Win10

[书籍](https://yeasy.gitbooks.io/docker_practice/image/pull.html)
[下载](https://cloud.docker.com/)
[CSDN](https://blog.csdn.net/zhang197093/article/details/78643708)

由于Docker是运行在linux系统上的，所以要想在windows上运行docker，需要借助虚拟机，老的[Docker Toolbox](https://www.docker.com/products/docker-toolbox)使用Oracle VM VirtualBox 来运行一个简化的linux系统，而目前的[Docker CE for Windows](https://store.docker.com/editions/community/docker-ce-desktop-windows)则是使用微软自带的 Hyper-V（从Win8开始）虚拟机组件。

所以在安装Docker CE for Windows时，会帮你打开Hyper-V组件（默认是关闭的），这会和你的VirtualBox冲突，导致VirtualBox无法正常运行，解决办法就是关闭Hyper-V功能（卸载Docker CE for Windows时并不会自动帮你关闭）

* 坑点1
类似的错误, 大可能是由于你使用了不在已有镜像服务器的镜像: 此时需要添加合适的镜像服务器, 或是换一个
``` shell
Get https://registry-1.docker.io/v2/: net/http: request canceled while waiting for connection
(Client.Timeout exceeded while awaiting headers)
```

* [Docker 进阶](https://my.oschina.net/ykbj/blog/1595328)
* [使用Docker本地运行jekyll](https://archerwq.github.io/2017/09/21/setup-jekyll-locally-with-docker/)(老版本 失败告终)
* [使用Docker本地运行jekyll](https://annatarhe.github.io/2016/11/27/all-i-know-about-docker.html)(老版本 折腾了至少一小时 运行起来了 但自己的博客并没有运行起来)
* [官网Doc](https://docs.docker.com/docker-for-windows/#docker-settings-dialog)(扣由桌面程序处启动)

* [更改镜像存储目录](https://blog.csdn.net/u013948858/article/details/80811986)
* [安装软件失败](https://juejin.im/post/59a8f9e0f265da24797b7da0)
* [更改WSL 或者 Docker的位置](https://forums.docker.com/t/where-are-images-stored/9794/10)
* [无名镜像](https://www.oschina.net/question/1050447_165040)
```shell
< none >
```

* 简单解释
1. dockerfile: 构建镜像；服务除了可以基于指定的镜像，还可以基于一份 Dockerfile
2. docker run: 启动容器；
3. docker-compose: [启动服务](https://www.jianshu.com/p/2217cfed29d7)；

- Github Gist 2018年12月左右
