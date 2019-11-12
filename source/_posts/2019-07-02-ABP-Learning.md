---
title: ABP-Learning
tags:
  - 流水帐
description: 上手ASP.NET Boilerplate (ASP.NET样板项目)
categories:
  - DotNet
date: 2019-07-02 20:45:29
---

# 前言
- 本文**几乎**完全按照时间顺序记录, 可以视为就是**流水帐**啦
- 流水帐的好处在于, 仅需少量背书+符合认知规律

# 数据库环境
[Oracle数据库11gR2下载地址 - WebLogic Android 博客](https://beansoftapp.github.io/2010/11/18/oracle%E6%95%B0%E6%8D%AE%E5%BA%9311gr2%E4%B8%8B%E8%BD%BD%E5%9C%B0%E5%9D%80/)
将注册表中的服务对应的表项删除后,重启即可看到服务项被删除

[Oracle 11g安装步骤详谈 - starskyhu - 博客园](https://www.cnblogs.com/hoobey/p/6010804.html)
[Oracle 十全大补汤 | AMAN's BLOG](https://jlhxxxx.github.io/oracle-rudiment.html)

执行sqlplus报错`SP2-0750: You may need to set ORACLE_HOME to your Oracle software directory`ORACLE_HOME环境变量未配置好: 需要到app...home这一级
`ORA-12560: TNS: 协议适配器错误`未解决 重装oracle
[Windows下把Oracle卸载干净 - 简书](https://www.jianshu.com/p/3d84efb92484)

`INS-13001 环境不满足最低要求` 忽略就行 也可参考更改配置文件(但是没看明白)
[Oracle——异常集 · IanEiU](https://ianeiu.github.io/2018/09/19/oracle%E5%BC%82%E5%B8%B8%E9%9B%86/)

`OUI-10137`C:\Program Files\Oracle\Inventory没有删除(PS: 在这种情况下新生成的文件不用删除)
`在注册表中没有找到指定的主目录名` 据说是没有更改环境变量 但是这里是更改了的 或许和之前没有删除OUI-10137错误的文件有关

事后可登录 [Oracle Enterprise Manager](https://localhost:1158/em)
仅管理员才是可以登录到 Enterprise Manager 执行管理任务 (如设置封锁, 电子邮件通知调度) 的数据库用户。

![oracle安装成功结果](/assets/img/sharding/oracle/oracle安装成功结果.png)

然后使用**数据库管理软件**连接:

**Toad**是数据库管理及开发的极佳工具，简单的说就是oem+sqlplus+pl/sql developer

`错误 忘了怎么解决的了`
```
Cannot load OCI DLL:  DriveLetter:\app\username\product\11.2.0\instantclient_11_1\oci.dll
```
`错误 忘了怎么解决的了`
```
This product require Microsoft MSXML 4.20.9818.0 or above and will not be installed at this time. Please refer to the product release notes for specific requirements. Microsoft MSXML 4(msxml.msi) can be installed from the Microsoft download centre . 
Benchmark Factory® for Databases is a database replay and performance testing tool that stress tests your environment by simulating users and SQL transactions on the database. Developers and QA professionals use Benchmark Factory and Toad to test SQL and database code against development SLAs and scalability. DBAs use Benchmark Factory and Toad to replay database workload or utilize industry standard benchmarks to mitigate the risks of database upgrades, migrations or patch releases. 
```

- 坑(最前面是解决方案 链接的名称就是坑的描述)
	- `忽略`[Oracle安装错误ora-00922（缺少或无效选项）](http://blog.sina.com.cn/s/blog_5674f6d401012ekw.html)
	- `GK 如何安装 Oracle`[Windows下Oracle安装图解----oracle-win-64-11g 详细安装步骤](https://www.cnblogs.com/liuhongfeng/p/5267549.html)
	- `未安装客户端` [TOAD OR PLSQL 连接 ORACLE ，Toad报“No valid Oracle Client found”](https://blog.csdn.net/huoyunshen88/article/details/26725045)
	- `无效 Origin-Others`[oracle配置监听问题——注册表中没有OracleOraDb11g_home1TNSListener](https://blog.csdn.net/qq_35396447/article/details/78072218)
	- `删除注册表项后重启` [找不到OracleMTSRecoveryService](https://blog.csdn.net/weixin_37817685/article/details/60877927)
	- `忽略`[orapwd.exe Unable to find error file"%ORACLE_HOME%"\RDBMS\opw]
	- `忽略`INS-20802 Oracle Net Configuration Assistant 失败。[信息: Oracle Database Configuration Assistant 失败](https://blog.csdn.net/typa01_kk/article/details/40452647)

`GK: EF模型 和 ORM 的区别 -CSDN`
[ORM系列之Entity FrameWork详解](https://www.cnblogs.com/yaopengfei/p/9196962.html)


# C#编程入门
`有编程基础的话`这一部分 基本可以边上手边学的

`SK: Essential C# C# "本质论" filetype:pdf -博客 -baidu`
	[C#本质论](https://book.douban.com/subject/5243513/)

[整型数值类型（C# 参考）](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/builtin-types/integral-numeric-types)
[避免对C#中float，double，decimal的错误理解](https://www.cnblogs.com/EthanCai/archive/2008/07/06/1237012.html)

`SK: Google 搜索 问号`
[如何谷歌一个问号](http://www.kbase101.com/question/51213.html)
[Google Hacking————你真的会用Google吗？](https://zhuanlan.zhihu.com/p/22161675)
>"+"强制搜索其后的一个单词，可以取消之前说的Google对常用单词的忽视(AND逻辑)，
>但是大部分常用英文符号(如问号，句号，逗号等)无法成为搜索关键字，加强制也不行；

SO `SK: "decimal?"`是不行的, 要使用`SK: decimal 问号`
[C#中,为什么在值类型后面加问号](https://www.cnblogs.com/darrenji/p/3824857.html)
decimal?是可空类型就是可以将值设置为Null，decimal 不能设置为null
另见[Class LinqExtensions: InsertWithDecimalIdentity](https://linq2db.github.io/api/LinqToDB.LinqExtensions.html)


# DotNet入门

**背书**
>[ASP.Net -Wiki](https://zh.wikipedia.org/wiki/ASP.NET)是由微软在.NET Framework框架中所提供，开发Web应用程序的**类库**，
>封装在System.Web.dll文件中，显露出System.Web名字空间，并提供ASP.NET网页处理、扩展以及HTTP通道的应用程序与通信处理等工作，以及Web Service的基础架构。
>ASP.NET是ASP技术的后继者，但它的发展性要比ASP技术要强大许多。

>为了因应云端化所诱发的多作业平台集成与开发能力，微软特别开发一个新一代的 ASP.NET，称为 ASP.NET vNext，
>并于 2014 年命名为 ASP.NET 5，但随后于 2016 年将它更名为 **ASP.NET Core**，
>由于架构上的差异颇大，因此未来 ASP.NET 与 ASP.NET Core 将是分别发展与维护，
>Windows 平台的 ASP.NET 4.6 以上版本仍维持 Windows Only，但 ASP.NET Core 则是具有跨平台 (Windows, Mac OSX 与 Linux) 的能力。

## 问题多又多

`都不是什么大不了的问题 懒得归类+不多解释`

[virtual（C# 参考）](https://docs.microsoft.com/zh-CN/dotnet/csharp/language-reference/keywords/virtual)

`SK: Visual Studio 2017 C# 代码高亮 using "错误" -CSDN -程序错误 -插件 -更新 -调试`
	[?? 运算符（C# 参考）](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/operators/null-coalescing-operator)


`SK: VS2017 ASP.NET NUGET 程序集引用 報紅 但是程序可以正常運行`
	[解决.NET 项目引用类库出现黄色警告](https://blog.csdn.net/u012751272/article/details/79400008)
	[【Visual Studio】项目的引用显示黄色叹号](https://blog.csdn.net/weixin_33738555/article/details/85962141)


`SK: 如何 更改所引用的工程文件的.Net版本 感嘆號`
	[C# 工程中引用出现感叹号](http://www.voidcn.com/article/p-rmbmlvkk-rh.html)
	[C# 工程中引用出现感叹号](https://blog.csdn.net/CrackLibby/article/details/47665745)
	[VS中修改.net版本](https://blog.csdn.net/jl1134069094/article/details/51151429)

`SK: Microsoft.AI.Web 黄色叹号`
	[无法加载文件或程序集“Microsoft.AI.Web”或其依赖项之一。该系统找不到指定的文件](http://landcareweb.com/questions/25321/wu-fa-jia-zai-wen-jian-huo-cheng-xu-ji-microsoft-ai-web-huo-qi-yi-lai-xiang-zhi-yi-gai-xi-tong-zhao-bu-dao-zhi-ding-de-wen-jian)


`SK: 未能找到类型或命名空间名 "AutoMap From"`
	[VS的ASP.NET项目中cshtml关键词出错 红线，当前上下文中不存在名称](https://www.cnblogs.com/xdot/p/10432966.html)
	[c# – 命名空间不被识别(即使它在那里)](https://codeday.me/bug/20170611/24030.html)
	[解决Visual studio编写C#时“未能找到类型名称或命名空间名称XXX...”错误](https://blog.csdn.net/Mingyueyixi/article/details/54415902)


`SK: System.BadImageFormatException: 未能加载文件或程序集 或它的某一个依赖项。试图加载格式不正确的程序。。`
	'InstallUtil' 不是内部或外部命令，也不是可运行的程序
	"vcvars32.bat"
	[Installutil.exe（安装程序工具）](https://docs.microsoft.com/zh-CN/dotnet/framework/tools/installutil-exe-installer-tool)
	[未能加载文件或程序集“XXXXXX”或它的某一个依赖项。试图加载格式不正确的程序。](https://www.cnblogs.com/autumn/p/3575008.html)


```cmd
vsCommandPrompt32
: 然后出现类似的内容
>"C:\Program Files (x86)\Microsoft Visual Studio\2017\Professional\VC\Auxiliary\Build\vcvars32.bat"
**********************************************************************
** Visual Studio 2017 Developer Command Prompt v15.8.0
** Copyright (c) 2017 Microsoft Corporation
**********************************************************************
[vcvarsall.bat] Environment initialized for: 'x86'

: 之后就可以使用词命令安装服务了
InstallUtil ./WinService.exe
```


`SK: X ORA-28547：connection to server failed，probable Oracle Net admin error`
[用Navicat连接Oracle数据库时报错ORA-28547:connection to server failed, probable Oracle Net admin error - 不忘初心 - CSDN博客](https://blog.csdn.net/gaoying_blogs/article/details/45440797)

`SK: Navicat 连接 ORACLE`
[Navicat Premium 连接Oracle 数据库（图文教程） - 周江霄 - CSDN博客](https://blog.csdn.net/zjx86320/article/details/49464251)



`SK: 如何 测试 IIS Express Web API postman`
	[如何在ASP.NET Core Web API测试中使用Postman](https://www.toutiao.com/i6489186032729195021/)
	[使用 Postman 调试 ASP.NET Core 开发的 API - walterlv](https://blog.walterlv.com/post/use-postman-to-debug-asp-net-core-api.html)
	[教程：使用 ASP.NET Core MVC 创建 Web API](https://docs.microsoft.com/zh-cn/aspnet/core/tutorials/first-web-api?view=aspnetcore-2.2&tabs=visual-studio)

`SK: 当前不会命中断点 还未`
	[VS2017调试代码显示“当前无法命中断点，还没有为该文档加载任何符号”](https://blog.csdn.net/shakspers/article/details/78978017)
	[Visual Studio 当前不会命中断点的问题](https://www.cnblogs.com/MigCoder/p/3368319.html)
PS: `只改过部分配置 实在乱掉可以参考admin的VS配置 或还原`

[SK 在证书存储区中找不到清单签名证书 ](https://www.cnblogs.com/190196539/archive/2011/12/03/2272861.html)

`执行interfaceRpo.Get遇到异常(莫非是由于没有实现..?)`[“System.Reflection.AmbiguousMatchException”类型的异常在 mscorlib.dll 中发生](https://www.cnblogs.com/senyier/p/7298759.html)


## ABP框架
[ABP简单架构](https://www.processon.com/diagraming/5d19728ce4b014412aa8ddab)

`强调`对数据进行变动的是业务(Business), 仓储只实现查询, 数据变动已经被基础的仓储接口实现

### 基本使用
`SK: "IRepository" docs 教程`
[ABP 教程文档 1-1 手把手引进门之 AngularJs, ASP.NET MVC, Web API 和 EntityFramework（官方教程翻译版 版本3.2.5）含学习资料](https://www.cnblogs.com/yabu007/p/8134792.html)
[设计基础结构持久性层](https://docs.microsoft.com/zh-CN/dotnet/standard/microservices-architecture/microservice-ddd-cqrs-patterns/infrastructure-persistence-layer-design)

`SK: IRepository Query接口 用法`
[NopCommerce源码架构详解--EF数据访问实例详解](https://www.lanhusoft.com/Article/637.html)
[EntityFramework用法探索（四）Repository和UnitOfWork - 匠心十年 - 博客园](https://www.cnblogs.com/gaochundong/archive/2013/06/06/entityframework_usage_repository_unitofwork.html)

```C#
int cnt = db.GetTable<ORM_ENTITY_NAME>().Where(p => p.id == id).Delete();
return cnt > 0;
```

`SK: IRepository Get Single 区别`
[分享基于Entity Framework的Repository模式设计（附源码）](https://www.cnblogs.com/JustRun1983/p/3307774.html)

`SK: "System.Reflection.AmbiguousMatchException" (位于 mscorlib.dll 中`
[微软DotNet文档  AmbiguousMatchException Constructors ](https://docs.microsoft.com/zh-cn/dotnet/api/system.reflection.ambiguousmatchexception.-ctor?redirectedfrom=MSDN&view=netframework-4.8#System_Reflection_AmbiguousMatchException__ctor_System_String_System_Exception_)

---

### 单元测试
`吐槽`安装 xunit生成插件后即可自动创建模板(当然, 得改改)
`吐槽`另外 无法直接对Controller进行测试(估计需要开启服务, 且要引入HTTP以及测试的内容所处的项目 实际上项目跑起来后并不能执行测试)
`吐槽`测试Servise又需要登录...

[这应该是postman最详细的中文使用教程了](https://www.jianshu.com/p/77f4f9175028)
`SK: Postman 测试 文件接口`[postman测试上传文件](https://www.cnblogs.com/shimh/p/6094410.html)

`SK: xunit Microsoft.VisualStudio.TestTools.UnitTesting 区别`[C#单元测试，带你快速入门](https://www.cnblogs.com/zhaopei/p/UnitTesting.html)
[安装单元测试框架](https://docs.microsoft.com/zh-cn/visualstudio/test/install-third-party-unit-test-frameworks?view=vs-2019)
[Live Unit Testing 简介](https://docs.microsoft.com/zh-cn/visualstudio/test/live-unit-testing-intro?view=vs-2019)
`SK VS 右键创建 Xunit 单元测试`
	[使用xUnit为.net core程序进行单元测试(1)](https://www.cnblogs.com/cgzl/p/8283610.html)
	[Visual Studio 2017 优雅单元测试](https://jingyan.baidu.com/article/6b97984dd9adb31ca2b0bfe0.html)

[代码质量随想录（六）用心写好注释](http://www.ituring.com.cn/article/8242)
[代码质量随想录（六）用心写好注释](https://codecafe1984.wordpress.com/2012/08/04/thinking_in_code_quality_6_write_elegant_comments_zh_cn/)

在持久仓库调用
1. [DataContext.GetTable<EntityType> Method](https://docs.microsoft.com/zh-CN/dotnet/api/system.data.linq.datacontext.gettable?view=netframework-4.8)
2. Query<EntityType>
3. Excute<EntityType>

当<EntityType>与仓库实际的EntityType不符时(即直接执行任何非声明仓库的sql语句)**Xunit单元测试**都会出现以下类似的错误
```C#
System.Reflection.TargetInvocationException
System.UnauthorizedAccessException
```
使用以下语句后可以保证
```C#
// IUnitOfWorkManager中IUnitOfWorkCompleteHandle Begin();
using (var uow = _unitOfWork.Begin())
{
	var result = _testerService.TestFun(entity);
	Assert.True(result != null, "测试成功!");
	// IUnitOfWorkCompleteHandle中void Complete();
	uow.Complete();
}
```

`SK: ABP 联查 IRepository`
- `无果`[ABP 数据库 -- ABP&EF中的多表、关联查询](https://www.cnblogs.com/alunchen/p/6835297.html)这个类似JPA的语法

`SK: IUnitOfWorkCompleteHandle Begin()`[ABP拦截器之UnitOfWorkRegistrar(二)](https://www.bbsmax.com/A/kmzLPjobzG/)
>如果一个带工作单元的方法调用了另外一个带工作单元的方法的时候，那么这两个方法是会共享相同的连接和事物的，并且第一个调用的方法管理这个工作单元，第二个进行复用，所以上面的这个ICurrentUnitOfWorkProvider接口主要是为了解决多个工作单元互相调用的问题。
[VS中如何添加自定义 代码片段 ](https://blog.csdn.net/guo13313/article/details/50608080)

单元测试报告显示
`System.InvalidOperationException : 序列不包含任何元素` 
	这个貌似是由于没有查询到元素(但加上后面的关联单元语句后会返回null)
`Message: System.NullReferenceException : 未将对象引用设置到对象的实例。` 
	使用了Single方法`Gets exactly one entity with given predicate. Throws exception if no entity or more than one entity.`


```C#
public class NameRepository : RepositoryBase<Name_Table>, INameRepository{
	// implement
}
// Name必须相同, 否则会
Message: Castle.MicroKernel.Handlers.HandlerException : Can't create component 'Sample.Abp.Service.NameService' as it has dependencies to be satisfied.

'Sample.Abp.Service.NameService' is waiting for the following dependencies:
- Service 'Sample.Abp.IRepositories.NameRepository' which was not registered.
```
`SK: C# 类似 org.springframework.beans BeanUtils.copyProperties 的方法`[慎用BeanUtils的对象拷贝方法](https://blog.csdn.net/q649381130/article/details/78064650)

#### 初始化测试资源

[C# 析构函数（Destructor）和终结器（Finalizer）——托管资源的释放](https://www.cnblogs.com/liuning8023/archive/2012/07/22/2603819.html)
->`官方`[终结器（C# 编程指南）](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/classes-and-structs/destructors)
**我们只能知道GC会回收这两个对象，但在.NET中，由于GC的存在，究竟何时调用析构函数我们是不能确认的。 **

[.NET 单元测试样例 (NUnit工具)](https://blog.csdn.net/cpcpc/article/details/6185946)

#### 释放资源

`Xunit.Abstractions.IAfterTestFinished;`
`SK: XUnit After Test Finished`[Run code once before and after ALL tests in xUnit.net](https://stackoverflow.com/questions/13829737/run-code-once-before-and-after-all-tests-in-xunit-net)
`SK: C# lambda 表达式`[Lambda 表达式（C# 编程指南）](https://docs.microsoft.com/zh-CN/dotnet/csharp/programming-guide/statements-expressions-operators/lambda-expressions)

最后发现 官方的文档中: 
```C#
//
// 摘要:
//     提供一种用于释放非托管资源的机制。 若要浏览此类型的.NET Framework 源代码，请参阅Reference Source。
[ComVisible(true)]
public interface IDisposable
{
		//
		// 摘要:
		//     执行与释放或重置非托管资源关联的应用程序定义的任务。
		void Dispose();
}
```

于是只需要重载Dispose方法就ok
`xunit错误也会执行 其他没试过`

最后: 
[c# – 使用XUnit断言异常](https://codeday.me/bug/20180822/226609.html)

---

### IIS
`SK: 未找到WAS 服务`[在计算机“.”上没有找到WAS服务](https://jingyan.baidu.com/article/15622f2410f770fdfcbea5d3.html)
[HTTP 错误 404.0 - Not Found](https://www.cnblogs.com/ggll611928/p/6525202.html)
