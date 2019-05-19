---
layout: post
title:  "Github Pages"
image: ''
date:   2018-12-9 17:22:31
tags:
- docker
description: 'GitHubPages'
categories:
- Learning
---

# Main Content
## What
1. 这是Github的吉祥物
![章鱼喵 测试](/assets/20190518133042898_20975.jpg)
2. [GithubPages帮助文档](https://help.github.com/en/articles/configuring-a-publishing-source-for-github-pages)的大意是说有三种 GithubPages:
    1. 遵循存储库命名方案username.github.io 或 orgname.github.io
        - 这种只能从master发布
    2. 从任意仓库的master分支上的/docs文件夹发布GitHub页面站点, 前提: 具有master分支，并且存储库必须
        - 在存储库的根目录中有一个/docs文件夹
        - 不遵循情形1的命名方式
     3. 从不遵循情形1命名方式的仓库的 master 或 gh-pages 分支发布
         -  创建对应分支后，可以将其中一个设置为发布源
     4. 如果都不是则发布源将设置为None, 站点不会发布

## How
### Create


## Why
1. 方便
2. 实惠
3. 等等

---
# Reference

## SEK
1. Bundler::HTTPError Could not fetch specs from https://gems.ruby-china.org/
2. 替换 Docker Ruby 源

## Links
1. [Gist](https://gist.github.com/SailHe/498aa5fbccb261a3e074a76296fb41d8)
2. [HomePage](https://github.com/sailhe)
3. [在Jekyll主题中自定义CSS和HTML](https://help.github.com/articles/customizing-css-and-html-in-your-jekyll-theme/)

## Else
1. Build an image from a Dockerfile
这是刚开始摸索Github Pages时使用别人的映像的shell
```Shell
docker build -t jekyll-local .
```
