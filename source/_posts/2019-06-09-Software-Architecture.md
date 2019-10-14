---
title: Software-Architecture
tags:
  - SoftwareArchitecture
description: 软件架构概念
categories:
  - Induction
date: 2019-06-09 19:57:00
---

**适合对软件架构已有一个感性的认识的读者**

- [软件架构](https://zh.wikipedia.org/wiki/软件架构) 是有关软件整体结构与组件的抽象描述，用于指导大型软件系统各个方面的设计。
- 组成

- 常见概念
  - 软件组件(构件)
  - 连接器
  - 风格 (体系结构风格/架构风格): 用于指导如何将系统中的各个模块和子系统有机的结合为一个完整的系统。
  - 软件框架(体系结构框架)
    - 中间件集成框架
    - 对象中间件
  - [设计模式](https://zh.wikipedia.org/zh-cn/设计模式_(计算机)): 是对软件设计中普遍存在（反复出现）的各种问题，所提出的解决方案。
  - 软件架构模式
      - MVC
          - 控制器（Controller）- 负责转发请求，对请求进行处理。
          - 视图（View） - 界面设计人员进行图形界面设计。
          - 模型（Model） - 程序员编写程序应有的功能（实现算法等等）、数据库专家进行数据管理和数据库设计(可以实现具体的功能)。


- 描述

> **软件架构**是一个系统的草图, 其描述的对象是直接构成系统的抽象组件。
> 各个**组件之间的连接**则明确和相对细致地描述**组件之间的通讯**。
> 在实现阶段，这些抽象组件被细化为实际的组件，比如具体某个类或者对象。
> 在面向对象领域中，组件之间的连接通常用**接口**来实现。

- 职业

>软件架构师
  1. 与客户商谈概念上的事情
  2. 与经理商谈广泛的设计问题
  3. 与软件工程师商谈创新的结构特性
  4. 与程序员商谈实现技巧，外观和风格。

传统的BS/CS结构下存在多台服务器, 即称为分布式

[软件构架、架构和框架的区别](https://my.oschina.net/duansheli/blog/292288) -> [原文](https://blog.csdn.net/nizhigang2000/article/details/58371)
[软件体系结构](https://blog.csdn.net/louxuez/article/details/9116755)
[几种常见的软件架构风格介绍](https://wxs.me/2069)

## 架构库
以库的源码语言为准(多个则取占比最大的)
### Python

`Repo`[Cookiecutter](https://github.com/cookiecutter/cookiecutter)
一个基于Python的命令行工具, 可以以各种模板为原型建立python, C, Java等语言的工程
`教程`[让你的项目模板化和专业化 - Cookiecutter ](https://betacat.online/posts/2017-08-16/cookiecutter-intro/)