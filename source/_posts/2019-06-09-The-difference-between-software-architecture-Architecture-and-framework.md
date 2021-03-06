---
title: The-difference-between-software-architecture-Architecture-and-framework
tags:
  - 架构
description: 软件构架、架构和框架的区别
categories:
  - 转载
date: 2019-06-09 20:16:00
---


# 软件构架、架构和框架的区别

## **软件框架**
(Software Framework)介绍 

>面向某领域（包括业务领域，如ERP，和计算领域，如GUI）的、可复用的"**半成品**"软件，它实现了该领域的共性部分，并提供一系列定义良好的可变点以保证灵活性和可扩展性。
 可以说，软件框架是**领域分析结果**的**软件化**，是领域内**最终应用系统**的**模板**。 

- 随着软件规模的扩大、应用的广泛和软件复用技术的发展，以子程序或类（Class）为单位的软件复用有许多不足：
>1. 子程序库日趋其庞大以致于使用人员难以掌握，
 1. 大多数类粒度很小，且其自身往往不能完成有用的功能。

这一问题迫使人们在复用中将一组类（或模块）及其交互作为一个整体来考虑，由此出现了软件框架。 

- 软件框架至少包含以下组成部分： 
>1. 一系列完成计算的**模块**，在此称为**构件**。 
 2. 构件之间的关系与**交互机制**。 
 3. 一系列**可变点**（也称**热点**，**Hot-spots**，或**调整点**）。 
 4. 可变点的**行为调整机制**。 

开发人员通过软件框架的**行为调整机制**，将领域中具体应用所特有的软件模块绑定到该软件框架的可变点，从而得到最终应用系统，这一过程称为**软件框架的例化（instantiation）**。
通过软件框架的使用，开发人员可将主要精力放在应用所特有的模块的开发上，从而大大提高了软件生产率和质量。 


软件框架的**行为调整机制**是指**如何针对**具体的应用**调整**该框架的**可变部分**、如何在**可变点**加入特定应用模块所采用的方法和规则。

- 行为调整机制可分为四种：
>1. 模板参数化。软件框架提供代码自动生成工具，该工具根据用户设置的参数自动生成所需的代码。 
 2. 继承和多态。通过面向对象中的子类继承和重载，在子类中加入新的功能或改变父类的行为。 
 3. 动态绑定。在运行时刻动态绑定所需的对象服务，可通过软件模式技术实现。 
 4. 构件替换。通过替换框架中可插拔的构件来加入业务特定的功能， 

不同于一般的可复用软件制品，软件框架的一个显著特点是逆向控制（Inversion of Control），在复用过程中，前者需被显式调用，控制是在应用特定的模块中，软件框架则不然，应用开发人员只要将应用特定的模块绑定到框架内，框架则根据自己的交互机制自动调用该模块，控制由框架负责。 

- 软件框架有很多种。

>按其应用的范围可分为： 
 1. 系统基础设施框架。用于简化系统级软件的开发，如操作系统、用户界面、语言处理等，典型例子为MacApp, Microsoft’s MFC等。 
 2. 中间件集成框架。用于组装分布式应用和构件，典型例子为Microsoft’s DCOM, JavaSoft’s RMI, OMG’s CORBA等 
 3. 企业应用框架。用于各类应用领域，如电信、制造业、金融等。 

>按其表现形态可分为： 
 1. 白盒框架。支持白盒复用，大型的类库或子程序库通常均提供白盒框架来协助复用。 
 2. 黑盒框架。支持黑盒复用。中间件集成框架一般为黑盒框架。


---


## **构架**和**架构**
也就是通常所说的**软件体系结构(software architecture)**.

体系结构一般包括三个部分:
  - 构件,用于描述计算;
  - 连接器,用于描述构件的连接部分;
  - 配置,将构件和连接器组成一个有机整体.
`对体系结构比较严谨比较认可的定义可参见＜软件工程技术概论＞（科学出版社）．`
>**体系结构**与**框架（Framework)**的区别与联系如下： 
 1. 呈现形式不同．体系结构的呈现形式是一个**设计规约**，而框架则是**程序代码**． 
 2. 目的不同．体系结构的首要目的大多是**指导一个软件系统的实施与开发**；而框架的首要目的是为**复用**．因此，**一个框架可有其体系结构**，用于指导该框架的开发，反之不然． 
 3. 有种特殊的体系结构, **DSSA(领域特定体系结构）**其首要目的也是为了复用． 
 4. 有个叫**体系结构风格**的东西，将它用程序代码实现后就成了Corba,COM之类的东西，它们俩叫**体系结构框架**，也叫**中间件集成框架**，又有人愿意叫它**对象中间件**


---


## 什么是模式？什么是框架？
（简述） ――UB （UB5023@MSN.COM） 2003-6-6

现在软件设计里到处都是模式，框架。有次朋友问什么是模式？我也在学习中，就我的学习经验，给出以下小结。（注意：个人观点，仅供参考，欢迎指正。）


1. 什么是模式？
> 模式，即pattern。其实就是解决某一类问题的方法论。你把解决某类问题的方法总结归纳到理论高度，那就是模式。
 Alexander给出的经典定义是：每个模式都描述了一个在我们的环境中不断出现的问题，然后描述了该问题的解决方案的核心。通过这种方式，你可以无数次地使用那些已有的解决方案，无需在重复相同的工作。
 模式有不同的领域，建筑领域有建筑模式，软件设计领域也有设计模式。当一个领域逐渐成熟的时候，自然会出现很多模式。

2. 什么是框架？
>框架，即framework。其实就是某种应用的半成品，就是一组组件，供你选用完成你自己的系统。简单说就是使用别人搭好的舞台，你来做表演。而且，框架一般是成熟的，不断升级的软件。

3. 为什么要用模式？
>因为模式是一种指导，在一个良好的指导下，有助于你完成任务，有助于你作出一个优良的设计方案，达到事半功倍的效果。而且会得到解决问题的最佳办法。

4. 为什么要用框架？
>因为软件系统发展到今天已经很复杂了，特别是服务器端软件，设计到的知识，内容，问题太多。
 在某些方面使用别人成熟的框架，就相当于让别人帮你完成一些基础工作，你只需要集中精力完成系统的业务逻辑设计。
 而且框架一般是成熟，稳健的，他可以处理系统很多细节问题，比如，事物处理，安全性，数据流控制等问题。
 还有框架一般都经过很多人使用，所以结构很好，所以扩展性也很好，而且它是不断升级的，你可以直接享受别人升级代码带来的好处。

框架一般处在低层应用平台（如J2EE）和高层业务逻辑之间的**中间层**。

5. 软件为什么要分层？
>为了实现“高内聚、低耦合”。把问题划分开来各个解决，易于控制，易于延展，易于分配资源…总之好处很多啦：）。

---

**以下所述主要是JAVA，J2EE方面的模式和框架：**

1. 常见的设计模式有什么？
> 首先，你要了解的是GOF的《设计模式--可复用面向对象软件的基础》一书（这个可以说是程序员必备的了），注意：GOF不是一个人，而是指四个人。
  它的原意是Gangs Of Four,就是“四人帮”，就是指此书的四个作者：Erich Gamma,Richard Helm，Ralph Johnson,John Vlissides。
  这本书讲了23种主要的模式，包括：抽象工厂、适配器、外观模式等。
  还有其他的很多模式，估计有100多种。

**软件设计模式太多，就我的理解简单说一下最常见的MVC模式。**
`本人注: MVC是架构模式或者说软件设计理念 并非简单的软件设计模式 前者显然解决的问题更加抽象 应用也更广泛`

MVC模式是1996年由Buschmann提出的：

- 模型（Model）：就是封装数据和所有基于对这些数据的操作。
- 视图（View）：就是封装的是对数据显示，即用户界面。
- 控制器（Control）：就是封装外界作用于模型的操作和对数据流向的控制等。

另外：
>RUP（Rational Unified Process）软件统一过程，XP（Extreme Programming）极端编程，这些通常被叫做“过程方法”，是一种软件项目实施过程的方法论，它是针对软件项目的实施过程提出的方法策略。也是另一个角度的模式。


2. 常见的JAVA框架有什么？

|  简称   |             全称              | 主要应用方面 |        主要应用技术        |                             出处                             | 简述 |  费用   |
| ------- | ----------------------------- | ----------- | ------------------------- | ------------------------------------------------------------ | ---- | ------ |
| WAF     | WEB APPLICATION FRAMEWORK     | EJB层[9]     | EJB等                     | [blueprints](http://java.sun.com/blueprints/code/index.html) | [1]  | 免费    |
| Struts  |                               | WEB层       | JSP,TagLib,JavaBean,XML等 | [struts](http://jakarta.apache.org/struts/index.html)        | [2]  | 免费    |
| Turbine |                               | WEB层       | servlet等                 | [turbine](http://jakarta.apache.org/turbine/index.html)      | [3]  | 免费    |
| COCOON  |                               | WEB层       | XML，XSP，servlet等       | [cocoon](http://cocoon.apache.org/2.0/)                      | [4]  | 免费    |
| ECHO    |                               | WEB层       | servlet等                 | [echo](http://www.nextapp.com/products/echo/)                | [5]  | 免费    |
| JATO    | SUN ONE Application Framework | WEB层       | JSP,TagLib,JavaBean等     | [sun](http://www.sun.com)                                    | [6]  | 免费    |
| TCF     | Thin-Client Framework         | JAVA GUI    | JAVA application等        | [tcf](http://www.alphaworks.ibm.com/tech/tcf)                | [7]  | 收费[8] |

**简述WAF+STRUTS结合的例子**：
WEB层用STRUTS，EJB层用WAF：
JSP(TagLib)->ActionForm->Action->
Event->EJBAction->EJB->DAO->Database
JSP（TagLib） (forward)<-Action<-EventResponse<-

- 拓展
1. 这是SUN在展示J2EE平台时所用的例子PetStore(宠物商店系统)里面的框架。是SUN蓝皮书例子程序中提出的应用框架。它实现了 MVC和其他良好的设计模式。SUN的网站上有技术资料，最好下载PetStore来研究，WEBLOGIC里自带此系统，源码在bea/weblogic700/samples/server/src/petstore。这是学习了解J2EE的首选框架。
2. 这是APACHE的开源项目，目前应用很广泛。基于MVC模式，结构很好，基于JSP。Jbuilder8里已经集成了STRUTS1.02的制作。
3. 这是APACHE的开源项目。基于SERVLET。据说速度比较快，基于service（pluggable implementation可插拔的执行组件）的方式提供各种服务。
4. 这是APACHE的一个开源项目。基于XML，基于XSP（通俗地说，XSP是在XML静态文档中加入Java程序段后形成的动态XML文档。）。特点是可以与多种数据源交互，包括文件系统，数据库，LDAP，XML资源库，网络数据源等。
5. nextapp公司的一个开源项目。基于SERVLET。页面可以做的很漂亮，结合echopoint，可以作出很多图形效果（里面用了jfreechart包）。使用SWING的思想来作网页，把HTML当作JAVA的类来做。但是大量使用Session，页面分帧（Frame）很多,系统资源消耗很大。
6. 这是SUN推出的一个商业性框架，一看名字就知道是结合SUN ONE的平台推出的。我下载了JATO2.0看了一下，感觉有些简单，使用了JSP＋TagLib+JavaBean。如他的DOC所说JATO是适合用在小的WEB应用里。
7. 这是IBM出的一个框架。基于MVC模式，基于JAVA Application。推荐一篇介绍文章：http://www-900.ibm.com/developerWorks/cn/java/j-tcf1/index.shtml
8. (每个企业对象license:2000美元)
9. (WEB层也有，但是比较弱)


其实本文的目的在于“抛砖引玉”，希望各路高手请你们把各种框架的特点和出处罗列一下 ，供大家参考，选用。

---

**本文转载自：https://blog.csdn.net/nizhigang2000/article/details/58371**
**始见于: https://my.oschina.net/duansheli/blog/292288**
- 排版(优化阅读体验)
- 无内容减少
