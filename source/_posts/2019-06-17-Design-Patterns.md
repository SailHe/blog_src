---
title: Design-Patterns
tags:
  - DesignPatterns
  - TomCat
description: 介绍一点设计模式的知识
categories:
  - Induction
date: 2019-06-17 15:45:27
---


# 设计模式

## [观察者模式](https://zh.wikipedia.org/wiki/观察者模式)
是软件设计模式的一种。在此种模式中，一个**目标对象**管理所有相依于它的**观察者对象**，并且在它本身的状态改变时主动发出通知。这通常透过呼叫各观察者所提供的方法来实现。此种模式通常被用来实时事件处理系统.

观察者模式: 观察者(Observer)-目标主题(Subject)
别称: 
  - 发布-订阅(Publish/Subscribe)模式
  - 源-监听(Source/Listener)模式

实现时常用词汇:
  - 抽象-基础-具体
  - 目标(主题发布者/源)
  - 观察者(主题订阅者/监听者)

表面上, 它定义了一种一对多的依赖关系: 一个主题，多个观察者，当主题发生变化的时候，会主动的通知观察者，这样观察者便能针对主题发生的变化，执行某些对应的动作.
实际上, 一个观察者可以同时订阅多个主题, 因此是一种多对多的依赖关系.

### 通用类图
![Servlet事件机制-事件](/assets/img/sharding/design-pattern/Observer-pattern-class-diagram.png)
详细类图, 这张感觉命名好一点
![Servlet事件机制-事件](/assets/img/sharding/design-pattern/Observer-pattern-class-diagram-info.png)

#### 易混淆概念
Subject:
- 添附(Attach)：新增观察者到串炼内，以追踪目标对象的变化。<==> Add
- 解附(Detach)：将已经存在的观察者从串炼中移除。         <==> Delete
- 通知(NotifyObserver)：利用观察者所提供的更新函式来通知此目标已经产生变化。

Observer
- Notify <==> Update // 一个概念, 都是表示更新观察者状态


### Tomcat的观察者模式
此处讲述Tomcat中用到观察者模式的两个地方: Servlet事件机制 以及 生命周期管理机制, 当然整个 Tomcat 服务器中这种模式使用肯定远不止于此限于篇幅(事实上貌似容器本身也是一种发布者), 不予论述.

#### Servlet事件机制
Tomcat Servlet 中提供了很多种**事件观察者接口**，此处仅列举5个：
HttpSessionAttributeListener, ServletRequestAttributeListener, ServletContextAttributeListener, ServletRequestListener, ServletContextListener
如下图所示：
- 事件源
 ![Servlet事件机制-事件](/assets/img/sharding/tomcat/EventPublisher.png)
- 监听者
 ![Servlet事件机制-事件监听器](/assets/img/sharding/tomcat/EventListeners.png)

需要注意的是它们都继承于 EventListeners 接口, 这是java.util中的接口, 始于JDK1.1, 其是一个空接口, 什么也没写
这样实现不怎么现代化, 接下来看看Tomcat的生命周期中的观察者模式实现

#### 生命周期管理机制

> [Servlet容器的启动过程](https://www.jianshu.com/p/4e4eac05815f)
 ![Tomcat的容器体系](/assets/img/sharding/tomcat/Tomcat的容器体系.png)
 总之, 真正管理Servlet的容器是Context，一个Context对应一个Web工程，也就是webapps下的一个项目，Context中的Wrapper也就是包装后的servlet。
 一个web应用对应一个Context容器，当添加一个web应用的时候会创建一个StandardContext容器，并且做相关配置，其中最重要的是ContextConfig（实际上是一个监听器），这个类将负责整个web应用的解析工作，当 context容器的状态被更改时，ContextConfig会被通知，做相关解析工作，最后将这个容器加到父容器Host中。

以上是此模式的大概应用, 此处是类图
- 生命周期(源)
 ![Lifecycle](/assets/img/sharding/tomcat/Lifecycle.png)
- 生命周期监听器
 ![LifecycleListener](/assets/img/sharding/tomcat/LifecycleListener.png)
- 其它相关类, 用于传递事件状态, 等等, 仅列出主要的几个中的部分
 ![Lifecycle其它相关类](/assets/img/sharding/tomcat/Lifecycle其它相关类.png)



```java
// 注意: 实际源码远不及此 此处仅提取观察者模式中的关键部分, 作为 模式实现 和 理想模式 之间的对比
// Lifecycle: 生命周期是源目标
// LifecycleBase 是基础生命周期, 继承了基础源的类称具体源
// 监听者(LifecycleListener)与此类似, 故不赘述
public abstract class LifecycleBase implements Lifecycle {

    // 是发布者中的监听器们 此处使用List接口实现(PS: CopyOnWriteArrayList是ArrayList的线程安全变体)
    private final List<LifecycleListener> lifecycleListeners = new CopyOnWriteArrayList<>();
    // 当前生命周期源的状态
    private volatile LifecycleState state = LifecycleState.NEW;

    @Override
    // 添加一个监听器
    public void addLifecycleListener(LifecycleListener listener) {
        lifecycleListeners.add(listener);
    }

    @Override
    // 移除一个监听器
    public void removeLifecycleListener(LifecycleListener listener) {
        lifecycleListeners.remove(listener);
    }

    // 触发(通知)所有监听器, 与通用类图中的uptate/notifyObserves是一个意义
    protected void fireLifecycleEvent(String type, Object data) {
        // 将源作为引用随事件传入监听器
        LifecycleEvent event = new LifecycleEvent(this, type, data);
        for (LifecycleListener listener : lifecycleListeners) {
            listener.lifecycleEvent(event);
        }
    }
}
```

## 参考
Wiki: https://zh.wikipedia.org/wiki/设计模式_(计算机)

[观察者模式](https://www.cnblogs.com/luohanguo/p/7825656.html)
`这是一个系列`[Tomcat生命周期管理与观察者模式](https://www.jianshu.com/p/0092ee6e57ca)
[Tomcat 源码分析 项目启动 (基于8.0.5)](https://www.jianshu.com/p/f987141887bb)
[ 从tomcat中学习观察者模式 ](https://my.oschina.net/u/227422/blog/66213)

