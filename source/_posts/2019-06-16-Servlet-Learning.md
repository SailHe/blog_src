---
title: Servlet-Learning
tags:
  - Servlet
description: 记录学习Servlet相关的知识的情况
categories:
  - Experience
date: 2019-06-16 11:56:22
---

# 基础概念
[JavaBeans](https://zh.wikipedia.org/wiki/JavaBeans)是Java中一种特殊的类，可以将多个对象封装到一个对象（bean）中。特点是**可序列化**, **提供无参构造器**, **提供getter方法和setter方法**访问对象的属性。名称中的“Bean”是用于Java的**可重用软件组件**的惯用叫法。 

[浅谈model, orm, dao和active record的区别](https://www.jianshu.com/p/f643f1fa1a20)

[Apache Struts 2](https://zh.wikipedia.org/wiki/Struts2)是一个用于开发Java EE网络应用程序的开放源代码网页应用程序架构。它利用并延伸了Java Servlet API，鼓励开发者采用MVC架构。 


# [Java Servlet](https://zh.wikipedia.org/wiki/Java_Servlet)
>Servlet（Server Applet），全称Java Servlet，未有中文译文。是用Java编写的服务器端程序。
 其主要功能在于交互式地浏览和修改数据，生成动态Web内容。狭义的Servlet是指Java语言实现的一个接口，**广义的Servlet是指任何实现了这个Servlet接口的类，一般情况下，人们将Servlet理解为后者。**
 Servlet运行于支持Java的应用服务器中。从实现上讲，Servlet可以响应任何类型的请求，但**绝大多数情况下Servlet只用来扩展基于HTTP协议的Web服务器。**
 最早支持Servlet标准的是JavaSoft的Java Web Server。此后，一些其它的基于Java的Web服务器开始支持标准的Servlet。 
 ![Life of a JSP file](/assets/img/sharding/JSPLife.png)
 ![ModelViewControllerDiagramZh](/assets/img/sharding/ModelViewControllerDiagramZh.png)

>**工作模式**
  客户端**发送请求**至服务器
  服务器**启动**并**调用**Servlet，Servlet根据客户端请求**生成响应内容**并将其传给服务器
  服务器将**响应返回**客户端
  其他
以上引用自标题指向的wiki, 无内容改动, 简而言之, Servlet是用来响应客户端请求然后生成Html的服务端java小程序, 这是Javaweb的根本
HttpServlet拓展了Servlet
Java服务器页面([JSP](https://zh.wikipedia.org/wiki/JSP))又拓展了HttpServlet
  其功能是使用HTML的书写格式，在适当的地方加入Java代码片段,
  即: Servlet是在服务器端java程序中写Html
      JSP是在JSP页面中`感觉不能说是前端`书写java代码, 类似于JavaScript脚本, 只是后者不能直接调用与服务器相关的内容, 比如文件`不是指客户端的文件`或数据库

[Servlet 工作原理解析](https://www.ibm.com/developerworks/cn/java/j-lo-servlet/index.html#N10085)
- Servlet - 接口 - 容器{ Jetty; Tomcat }
- 里面有类图; 时序图; 讲解详细, 此处就不再赘述

# [Tomcat](https://zh.wikipedia.org/zh-cn/Apache_Tomcat)

1. SpringBoot 内置 tomcat 依赖
2. 使用maven打成war包后使用外置tomcat启动
3. Tomcat提供了一个Jasper编译器用以将JSP编译成对应的Servlet。 

`SK`tomcat 启动  war包

`SK: 如何 下载 Tomcat 源码`[死磕tomcat源码(一)之源码下载与导入IDEA](https://www.jianshu.com/p/eb9f628cf82b)
-> [SRC-8.X](https://tomcat.apache.org/download-80.cgi)

# Links

'SK: Spring MVC 和 三层架构'[MVC 与三层架构](https://juejin.im/post/5929259b44d90400642194f3)

1. `太笼统`[Spring Boot - Tomcat容器部署](https://www.jianshu.com/p/a5195a08da3e)
2. [tomcat本地部署war包的方式](https://www.cnblogs.com/laogai/p/4935193.html)
3. [Tomcat部署java web项目,war包方式](https://www.jianshu.com/p/e48ae3b99573)
4. `SK: SpringMVC 和 Servlet`[Servlet 到 Spring MVC 的简化之路](https://juejin.im/post/5a9f3ddb5188255585071151)
5. [Spring Framework 整体架构](https://www.jianshu.com/p/3bd8b40400c9)
6. `SK: Spring MVC`[Spring MVC【入门】就这一篇！](https://www.jianshu.com/p/91a2d0a1e45a)
7. [99%的人理解错 HTTP 中 GET 与 POST 的区别](https://www.oschina.net/news/77354/http-get-post-different)
8. [MDN-GET](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Methods/GET)
9. [Spring、Struts、Hibernate框架之间的关系是什么以及怎么处理](https://blog.csdn.net/qq_24452475/article/details/51068258)
10. [关于SpringMVC和Struts2的区别](https://www.jianshu.com/p/f1e5f789939c)
11. [Struts1和Struts2的区别和对比](https://www.jianshu.com/p/3e7e40bde455)
12. `注意 MVC不是分层`[MVC模式](https://www.ruanyifeng.com/blog/2007/11/mvc.html)
13. [注意 MVC不是设计模式 而是架构模式 确切地说是一种理念](https://blog.csdn.net/zhangli_/article/details/50419783)
14. [注意 MVC不是框架模式 框架<=!=>架构](http://er.dadaaierer.com/?p=60)

## PS
Links[4]中提及的:
>模型（Model）：封装了应用程序的数据，通常由POJO类组成
Links[6]中提及的:
>M 代表 模型（Model） 模型是什么呢？ 模型就是数据，就是 dao,bean
**可能**容易误导读者
另外Links[6]中的命名方式也容易使初学者混淆**层**的概念, 比如DAO是**数据访问对象**, 而不是**数据访问层**
其中还使用了IDEA作为教程新建HelloWorld项目

`SK: MVC 模型到视图 虚线 意思`[MVC设计模式详解](https://blog.csdn.net/dqjyong/article/details/7697558)
 ->
`SK: MVC设计模式详解 "C对M" "C对V：Outlet"`[iOS学习之MVC设计模式的理解](https://www.cnblogs.com/blogoflzh/p/4684576.html)
 -> 
`Origin link`[IOS学习之——MVC模式](http://blog.sina.com.cn/s/blog_4a3dcc3901010062.html)


**下边者篇文章对MVC讲解的比较全面且深入, 解释了wiki的那张图**
`SK: https://upload.wikimedia.org/wikipedia/commons/thumb/f/f0/ModelViewControllerDiagramZh.png/200px-ModelViewControllerDiagramZh.png mvc`
[MVC，MVP，MVVM区别](https://www.jianshu.com/p/5e94569a430a)
`Origin Link`[MVC, MVP, MVVM比较以及区别(下)](https://www.cnblogs.com/JustRun1983/p/3727560.html)
[MVC, MVP, MVVM比较以及区别(上)](https://www.cnblogs.com/JustRun1983/p/3679827.html)


类似的搜索套路(但里面的内容需要商榷):
`SK: 设计模式 架构模式`[架构模式(Architectural Pattern)、设计模式(Design Pattern)、代码模式(Coding Pattern)](https://blog.csdn.net/cxzhq2002/article/details/78160530)
`SK: "架构模式(Architectural Pattern)、设计模式(Design Pattern)、代码模式(Coding Pattern)"`[架构模式(Architectural Pattern)、设计模式(Design Pattern)、代码模式(Coding Pattern)](https://www.cnblogs.com/duanxz/archive/2012/06/05/2536801.html)



[基于UML和ASP.NET实现三层B/S结构系统开发](https://www.cnblogs.com/HondaHsu/archive/2007/07/03/732754.html)中提到Domain是**系统中关键的类**

这里提到的三层的一个关系, 并非简单的上层依赖下层的关系, 由于依赖注入的存在, BLL可以使用DAL的接口而不是实现
`不过我始终认为三层架构只能是三层 名字不能再多加层了`[什么是三层架构？你真的理解分层的意义吗？](http://www.dalbll.com/Group/Topic/ArchitecturedDesign/4971)

这篇表现了 BS的三层{Browser-Server-DataBase} 和 应用三层{UI-BLL-DAL} 的关系, 但其中提到的 dao层 DAO 是对象不是层, DAO 属于 DAL层
[JavaWeb（六）之MVC与三层架构设计](https://www.cnblogs.com/zhangyinhua/p/7645581.html)

[几种常见的软件架构风格介绍](https://wxs.me/2069)

