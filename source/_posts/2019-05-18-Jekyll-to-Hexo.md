---
title: jekyll-to-Hexo
date: 2019-05-18 14:18:46
description: 将模板引擎从 Jekyll换为Hexo
tags:
    - 教程
categories:
    - 不务正业
---

---
# Main Content
将原有的静态博客生成器由 Jekyll 更换为 Hexo
## What
### 需求
1. 侧栏需要与 [VNote](https://github.com/tamlok/vnote) 的目录达成类似的用户体验
![例子](/assets/20190518143226654_24306.png)
2. 导航栏需要在顶部
3. 要有内部的搜索功能
4. 分类功能最好有层次, 表达出从属关系, [参考Demo](https://louisbarranqueiro.github.io/hexo-theme-tranquilpeak/all-categories/#posts-list-hack)
![例子](/assets/20190518144334801_25303.png)
5. 首页的文章概览不能超过两行, 一项最好不超过四行
6. 评论功能
    - 基于Github的Issue实现
    - 第三方
7. 代码要明了地显示出类别, 类似图中的Bash:
![例子](/assets/20190518143941912_4649.png)

## Why
- Hexo基于Node.js, 与本人已有的环境相符, 而且可以不用折腾Ruby
- 之前不使用Hexo是由于[此处](https://betacat.online/posts/2018-01-26/setup-jekyll-environment-on-windows/)提及Hexo不支持 Github Pages, 不过这两天发现可以
- 仍需要原来的sailhe.github.io域名, 而且但不想删掉记录

## How

### Context
- Windows 10
- Node.js - v8.11.1
- npm - 6.9.0
- 其它: 略

### 前置技能
1. Git的基本操作
2. npm的概念及其基本操作
3. Github的账户基本操作
4. SSH概念及其基本操作
5. GPG概念及其基本操作
6. WEB的基本概念以及与静态网页的区别
7. Hexo的基本使用

### Hexo的基本使用
1. [官方文档及教程](https://hexo.io/zh-cn/docs/)
2. [第三方教程](https://github.com/limedroid/HexoLearning)

### 部署的坑
**两个尖括号引发的心跳体验**
``` bash
$ hexo clean
$ hexo d

On branch master
nothing to commit, working tree clean
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
and the repository exists.
FATAL Something's wrong. Maybe you can find the solution here: http://hexo.io/docs/troubleshooting.html
Error: Spawn failed
    at ChildProcess.<anonymous> (E:\Projects\Source\Repos\_blog\blog\node_modules\hexo-util\lib\spawn.js:52:19)
    at emitTwo (events.js:126:13)
    at ChildProcess.emit (events.js:214:7)
    at ChildProcess.cp.emit (E:\Projects\Source\Repos\_blog\blog\node_modules\cross-spawn\lib\enoent.js:40:29)
    at Process.ChildProcess._handle.onexit (internal/child_process.js:198:12)
```

- **下面的Step是将如何找到解决方案的**
- **解决方案**就一句话: 去除_congif.yml内deploy下repo内的尖括号(也有可能是其它问题 比如空格什么的)

#### Step

1. 直接将原仓库的.git目录给复制过来然后执行以下命令, 没用.
```bash
$ git commit -m "balabala"
$ hexo d
```
2. 然后直接给push上去, 也没用
```bash
$ git push
$ hexo d
```
3. 那就只有可能是PGP的原因了(然而并不是)
4. 于是开始搜索
    - SEK[1]->基本都是部署教程
    - SEK[2]->基本都在说ssh
5. [官方错误帮助页面](https://hexo.io/zh-cn/docs/troubleshooting.html)也只提到git的问题
6. 无奈之下, 灵机一动, 仔细查看了下远端仓库: 这一顿骚操下来作只留下一个凌乱的仓库, 与本地完全不一样啊 (删除的东西没删掉)
![凌乱的仓库](/assets/20190518231911324_30952.png)
7. 这个[教程](https://juejin.im/post/5acf02086fb9a028b92d8652)的一句倒是提示了我
![提示](/assets/20190518232456899_11545.png)
8. 又瞧了瞧 Hexo的基本使用[2]的 [仓库页面](https://github.com/limedroid/limedroid.github.io), emmm? 应该是第1步没有git add -A的原因, 生疏了
9. 然后我使用之前未替换网页生成引擎时的本地备份(有备无患!), pull了下来, 然后删除所有, 之后将.deploy_git中的文件复制过去并操作push, emm然而还是没有用
10. 此刻我注意到了仓库里面deployments这个选项, 应该是这个问题, 上面那个例子是没有deployments的 (最后想起来不是自己的仓库是看不见部署环境的)
11. 好像又有点想法了, 不过有点晚了, 明天再说了
12. 第二天再次了解[GithubPages](/2018/12/09/GitHubPages/)后查看了下部署页面
![部署页面](/assets/20190519093755477_17493.png)
发现已经部署上去了, 估计Step[10]查看的时候还没部署上去, 也就是说那会就已经部署成功了
13. 不过hexo d的错误仍然存在, [这里面](http://wuwenliang.net/2017/01/26/转-针对github权限导致hexo部署失败的解决方案/)提到的错误倒是有点类似, 但是和之前的一样都是说的ssh的权限问题, 但是本人的ssh是可以正常使用的
![GPG密码在一段较短的时间内只用输入一遍](/assets/20190519100159752_15657.png)
14. 然而错误的主体仍未变化
```
You need a passphrase to unlock the secret key for
user: "SailHe <shell.sailhe@gmail.com>"
2048-bit RSA key, ID ???????, created 201.....

[master 687e0b9] Site updated: 2019-05-19 10:00:29
 14 files changed, 118 insertions(+), 66 deletions(-)
 create mode 100644 assets/20190518231911324_30952.png
 create mode 100644 assets/20190518232456899_11545.png
 create mode 100644 assets/20190519093755477_17493.png
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
// 以下错误雷同 略
```

15. 到目前为止, 直接在blog/.deploy_git目录下进行git操作是可行的, 而且很快就能在站点页面看到效果, 但根据[官网部署页面](https://hexo.io/zh-cn/docs/deployment.html#这一切是如何发生的？)所说, 应当可以自动push才对.
> 部署分支是_config.yml配置文件中指定的分支。Hexo会将生成的站点文件推送至该分支下，并且完全覆盖该分支下的已有内容。因此，部署分支应当不同于写作分支。
16. 想起来之前将部署分支改成 gh-pages 了, 改回master之后, emm, 错误变化了一点点, em?怎么让我手动push, 过分啊
``` bash
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean
Permission denied (publickey).
fatal: Could not read from remote repository.

Please make sure you have the correct access rights
// 以下错误雷同 略
```

17. 看了看[Hexo项目的issue](https://github.com/hexojs/hexo/issues?utf8=✓&q=is%3Aissue+Permission+denied+%28publickey%29.) 这个issue下全说的是ssh的问题, repo改成https形式的解决方案就不考虑了, 治标不治本, 与此错误匹配的issue是没有的, [类似](https://github.com/hexojs/hexo/issues?utf8=✓&q=is%3Aissue+Error%3A+Spawn+failed+spawn.js%3A52%3A19)的也只有几个

18. 根据远端push记录来看, Hexo d帮忙完成了commit操作 (从默认的Hexo提交消息可看出)
![远端push消息](/assets/20190519110502271_18760.png)

19. 精准搜索SEK[3], 结果只有4个, 的出的结论就是下面这条命令, 但未解决当前的问题 (在[变动_confit.yml](https://github.com/hexojs/hexo/issues/67)的情况下适用)
```bash
$ rm -rf .deploy_git && Hexo clean && hexo d -g
```
20. 按理说GPG只管的是commit的阶段啊, 现在的问题一直都是push失败, 也不是ssh的问题啊, 何况可以正常使用git push进行提交, 问题就是不能使用Hexo d, 而且仅仅是不能push...
```bash
$ ssh -T git@github.com
Hi SailHe! You've successfully authenticated, but GitHub does not provide shell access.
```
21. 由于网上所有信息几乎都指向ssh错误, 但此处ssh没毛病(就是其它地方都能用, 就这出问题了), 于是决定新建一个仓库用Hexo作下实验
22. 更换_config.yml部署的repo, 然后执行Step[21]的命令, 同样的问题
23. 最终, 终于从官方的部署视频教程Step[15]里面看出了一些端倪, 而且挖坑的人就是最开始的教程ORZ
![第三方写法](/assets/20190519122854010_27273.png)
![官方的写法](/assets/20190519124141838_26824.png)
![正确的写法](/assets/20190519123341993_31133.png)
emm, 没错, 多了俩尖括号...跟其它的shh什么的一点关系都没有, 就不评判那俩尖括号的好坏了, 可能是某种约定, 比如url使用<>, 分支使用[]括起来之类的

### 结论
1. 部署成功的提示(类似)
```Bash
Counting objects: 218, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (166/166), done.
Writing objects: 100% (218/218), 1.35 MiB | 597.00 KiB/s, done.
Total 218 (delta 40), reused 0 (delta 0)
remote: Resolving deltas: 100% (40/40), done.
To github.com:SailHe/sailhe.github.io.git
 + 687e0b9...44f6ead HEAD -> master (forced update)
Branch master set up to track remote branch master from git@github.com:SailHe/sailhe.github.io.git.
INFO  Deploy done: git
```
2. Hexo支持同目录写作以及部署, 但是不适应此处的情况, 此处的方案:
    - 原有的 sailhe.github.io 作为部署的仓库
    - 新建的 blog_src 作为写作仓库
3. 另外, 就此处的情况而言, 静态WEB, 比如Hexo与Jekyll的部署与有后端的WEB的部署是有点区别的, 最明显的就是无需启动服务, 前者的网页仓库是可以没有配置文件的.
4.  这个错误一般是由ssh引起的, 这类文章很多, 官方的issue列表里面也很多, 不过若确认ssh配置无误的话, 可能需要检查一下配置文件
5. 另外, 文档需要谨慎参考啊, 也许在某个作者并未意识到的地方会误导读者, 官方的这里好歹还加了一条注释帮助理解. 总的来说教程的内容尽量做到少重复为妙.
6. 如果是已经配置好了ssh, 就没必要用https的仓库链接了, 也是忘了
7. 结果证明及Hexo官网都提及:  对部署仓库是完全替换, 也就是说, 这个域名对应的原仓库是无法保留了, 但是好在之前有备份, git可是分布式的, 只要仓库还存在一个, 就仍能恢复
    - 删除刚刚新建的blog_src, 重建了一遍
    - 修改原本地仓库的/.git/config文件中的url选项为新的仓库url
    - 重新push即可恢复之前所有的提交记录(相当于把原仓库换了个名字)
    - 将刚刚仓库的内容全部删除(保留.git哟), 复制hexo的源码, 接下来再次push就可以啦, 所有记录都在哈哈
    ```bash
    $ git add -A # 增删文件可别忘了这个
    $ git commit -m "hexo init"
    $ git push # 查看一下Github此次提交感人的详情(平时还是要保证原子提交的说): Showing 581 changed files with 33,267 additions and 12,820 deletions.
    ```
8. 这一趟下来又是100来行的命令行... 接下来该整理下目录了, 顺带整理下Github的仓库, 差不多能正式开始写blog了
9. 删除了几个fork, 但没有commit的仓库, 比如Windows-classic-samples, 当时想干啥忘了, star一下, 删掉算了bootstrap-suggest-plugin
10. 话说原来Github的profile页面是可以自定义的...一直觉着是自动的, 今天整理仓库才发现不对劲
![自定义](assets/20190519194458598_11981.png)


---
# Reference
## SEK
1. GithubPages 如何部署 Hexo
2. hexo gpg 部署
3. Hexo Error: Spawn failed spawn.js:52:19 at emitTwo (events.js:126:13

## Links
1. [hexo-ssh](https://hzhenpeng.github.io/hexo-ssh.html)
2. [SEK3结果](https://www.icode9.com/content-4-189446.html)
3. [从Jekyll迁移到hexo](https://hexo.io/zh-cn/docs/migration.html)
4. [官方主题列表](https://hexo.io/themes/)
5. [赞赏参考](https://www.haomwei.com/about/)
6. [分类参考1](https://github.com/LouisBarranqueiro/hexo-theme-tranquilpeak)
7. [分类参考2](https://gaohaoyang.github.io/category/)

## Else
1. [VNote官网](https://tamlok.github.io/vnote/zh_cn/)
