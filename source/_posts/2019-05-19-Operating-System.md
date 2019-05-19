---
title: Operating-System
description: 归纳整理操作系统相关的知识与文档
date: 2019-05-19 22:06:09
tags:
    - 长期更新
---

**来源于Github Gist 创建于2018年12月左右 具体创建时间没注意**

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
sudo apt-get install zsh -y
chsh -s $(which zsh)
重启

--oh-my-zsh: zsh的配置项目
[Github参考](https://github.com/robbyrussell/oh-my-zsh)
git clone https://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh
//若存在.zshrc则备份
cp ~/.zshrc ~/.zshrc.orig
//创建模板.zshrc
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
chsh -s /bin/zsh


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
