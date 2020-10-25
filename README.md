**随着Java学习的不断深入，发现很多知识在脑海里都是一个个碎片，建此仓库的目的希望把零碎的知识点都整合起来，提高自己的学习效率。欢迎志同道合的朋友，一起来维护该仓库**

# 目录

  - [目录](#目录)
   - [网络基础](#网络基础)
     - [TCP协议](#tcp协议)
     - [HTTP/HTTPS](#httphttps)
   - [数据结构](#数据结构)
     - [树](#树)
       - [二叉树](#二叉树)
       - [红黑树](#红黑树)
       - [B、B 、B-树](#bbb树)
   - [设计模式](#设计模式)
      - [行为型模式](#行为型模式)
   - [Java基础](#java基础)
     - [语法](#语法)
     - [集合](#集合)
       - [HashMap](#hashmap)
     - [并发](#并发)
       - [概述](#概述)
       - [线程池](#线程池)
       - [AQS](#aqs)
       - [锁](#锁)
         - [Synchronized](#synchronized)
         - [ReentrantLock](#reentrantlock)
       - [J.U.C组件](#juc组件)
     - [IO](#io)
       - [NIO](#nio)
     - [JVM](#jvm)
       - [概述](#概述-1)
       - [垃圾回收器](#垃圾回收器)
       - [JVM调优](#jvm调优)
     - [JDK1.8 ](#jdk18)
     - [JDK发展](#jdk发展)
   - [框架](#框架)
     - [Spring](#spring)
       - [IOC](#ioc)
       - [AOP](#aop)
       - [动态代理](#动态代理)
       - [Spring MVC](#spring-mvc)
       - [Spring事务](#spring事务)
       - [常见问题](#常见问题)
     - [Spring Boot](#spring-boot)
     - [MyBatis](#mybatis)
   - [中间件](#中间件)
     - [注册中心](#注册中心)
       - [zookeeper](#zookeeper)
     - [RPC框架](#rpc框架)
       - [Dubbo](#dubbo)
     - [消息队列](#消息队列)
       - [总结](#总结)
         - [消息队列对比](#消息队列对比)
         - [笔记](#笔记)
       - [Kafka](#kafka)
         - [基本理解](#基本理解)
         - [深入理解](#深入理解)
         - [面试](#面试)
         - [总结](#总结-1)
       - [QMQ](#qmq)
   - [搜索引擎](#搜索引擎)
     - [ElasticSearch](#elasticsearch)
   - [配置中心](#配置中心)
   - [数据库](#数据库)
     - [Mysql](#mysql)
       - [概述](#概述-2)
       - [索引](#索引)
       - [锁和事务](#锁和事务)
       - [主从同步](#主从同步)
       - [查询优化](#查询优化)
     - [Redis](#redis)
     - [HBase](#hbase)
   - [分布式设计](#分布式设计)
     - [负载均衡](#负载均衡)
       - [算法](#算法)
         - [轮询与一致性HASH](#轮询与一致性hash)
     - [分布式锁](#分布式锁)
     - [分布式限流](#分布式限流)
     - [稳定性 &amp; 高可用](#稳定性--高可用)
       - [CAP与BASE](#cap与base)
     - [服务治理](#服务治理)
     - [分布式一致](#分布式一致)
   - [思想设计](#思想设计)
     - [微服务设计](#微服务设计)
     - [领域模型](#领域模型)
   - [错误排查](#错误排查)
     - [Http Client](#http-client)
   - [Review](#review)
   - [推荐书籍](#推荐书籍)
     - [Java](#java)
     - [Spring](#spring-1)
       - [Spring Boot](#spring-boot-1)
     - [代码风格](#代码风格)
     - [中间件相关](#中间件相关)
   - [面试](#面试-1)
     - [P6阶段](#p6阶段)
   - [个人成长](#个人成长)
   - [资料整理](#资料整理)



# 网络基础

## TCP协议

- [图解TCP协议中的三次握手和四次挥手](https://www.jianshu.com/p/9968b16b607e)

## HTTP/HTTPS

- [HTTPS加密原理](https://juejin.im/entry/5a9ac15bf265da239e4d8831)

# 数据结构

## 树

### 二叉树

- [3 分钟理解完全二叉树、平衡二叉树、二叉查找树](https://juejin.im/entry/6844903606408183815)

### 红黑树

- [漫画：什么是红黑树？](https://zhuanlan.zhihu.com/p/31805309)

- [30张图带你彻底理解红黑树](https://www.jianshu.com/p/e136ec79235c)

### B、B+、B*树

- [平衡二叉树、B树、B+树、B*树 理解其中一种你就都明白了](https://zhuanlan.zhihu.com/p/27700617)

# 设计模式

### 行为型模式

- [《设计模式——代理模式的思考》](https://blog.ganzhiqiang.wang/2019/02/17/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%E2%80%94%E2%80%94%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F%E7%9A%84%E6%80%9D%E8%80%83/#more)
- [《设计模式——观察者模式的思考》](https://blog.ganzhiqiang.wang/2019/01/20/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%E2%80%94%E2%80%94%E8%A7%82%E5%AF%9F%E8%80%85%E6%A8%A1%E5%BC%8F%E7%9A%84%E6%80%9D%E8%80%83/#more)
- [《设计模式——模板方法模式的思考》](https://blog.ganzhiqiang.wang/2019/01/13/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%E2%80%94%E2%80%94%E6%A8%A1%E6%9D%BF%E6%96%B9%E6%B3%95%E6%A8%A1%E5%BC%8F%E7%9A%84%E6%80%9D%E8%80%83/#more)

# Java基础

## 语法

- [精选30道Java笔试题解答](https://www.cnblogs.com/lanxuezaipiao/p/3371224.html)
  - 30道题中包含很多容易在日常开发中日益被忽视的细节

## 集合

- [ArrayList](https://juejin.im/post/5a02d2526fb9a04527250558)

### HashMap

- [HashMap? ConcurrentHashMap? 相信看完这篇没人能难住你！](https://crossoverjie.top/2018/07/23/java-senior/ConcurrentHashMap/)
- [Java7/8 中的 HashMap 和 ConcurrentHashMap 全解析](https://javadoop.com/post/hashmap)

## 并发

### 概述

- :star::star:[RedSpider1-concurrent](https://github.com/RedSpider1/concurrent)
- :star::star:[《Java并发》](https://github.com/CyC2018/CS-Notes/blob/master/notes/Java%20%E5%B9%B6%E5%8F%91.md)

### 线程池

- :star:[你都理解创建线程池的参数吗？](http://objcoding.com/2019/04/11/threadpool-initial-parameters/)

### AQS

- :star:[从ReentrantLock的实现看AQS的原理及应用](https://tech.meituan.com/2019/12/05/aqs-theory-and-apply.html)

### 锁

- [Java中的锁分类](https://www.cnblogs.com/qifengshi/p/6831055.html)
- ListenalbeFuture的使用总结](https://juejin.im/post/5cb48bcd6fb9a0687015c9c7)

#### Synchronized

- [Java经典面试题，你用过synchronized吗？它的底层原理是什么？](https://juejin.im/entry/6844904047430860813)
- [深入分析Synchronized原理(阿里面试题)](https://www.cnblogs.com/aspirant/p/11470858.html)

#### ReentrantLock

### J.U.C组件

- [Java进阶（七）正确理解Thread Local的原理与适用场景](http://www.jasongj.com/java/threadlocal/)

## IO

### NIO

- [Java IO](https://github.com/CyC2018/CS-Notes/blob/master/notes/Java%20IO.md)
- [详解NIO与BIO的区别，NIO的运行原理及并发使用场景](https://zhuanlan.zhihu.com/p/54829109)

## JVM

### 概述

- :star::star:[Java虚拟机](https://github.com/CyC2018/CS-Notes/blob/master/notes/Java%20%E8%99%9A%E6%8B%9F%E6%9C%BA.md)

### 垃圾回收器

### JVM调优

- [jvm优化必知系列——监控工具](https://juejin.im/post/6844903504402726920)
- [如何合理的规划一次jvm性能调优](https://juejin.im/post/6844903506093015053)

## JDK1.8+

- Lamda表达式与Stream流 [《Java Functional Programming Internals》](https://github.com/CarpenterLee/JavaLambdaInternals)

## JDK发展

- [Java 5，6，7，8，9，10，11新特性吐血总结](https://www.jianshu.com/p/38985b61ea83)

# 框架

## Spring

- [Spring Bean 生命周期](https://juejin.im/post/5ab1bf19f265da23771947f1)
- [Spring常用接口和类](https://blog.csdn.net/qq_35830949/article/details/79603622)

### IOC

- :star::star:[Spring IoC容器初的初始化过程](https://my.oschina.net/mindfind/blog/918515)
- [《Spring IOC 容器源码分析》](https://javadoop.com/post/spring-ioc)
- 【专栏】[JavaEE企业级分布式架构核心技术](https://zhuanlan.zhihu.com/p/41274946)
- 

### AOP

- [《Spring AOP 使用介绍，从前世到今生》](https://javadoop.com/post/spring-aop-intro)

### 动态代理

- [设计模式——代理模式的思考（Spring 部分）](https://blog.ganzhiqiang.wang/2019/02/17/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F%E2%80%94%E2%80%94%E4%BB%A3%E7%90%86%E6%A8%A1%E5%BC%8F%E7%9A%84%E6%80%9D%E8%80%83/#more)
- [Spring AOP中JDK和CGLib动态代理哪个更快？](https://juejin.im/entry/6844903673676431374)

### Spring MVC

- [SpringMVC执行流程及工作原理](https://www.jianshu.com/p/8a20c547e245)

### Spring事务

- [Spring 事务管理详解](http://www.mydlq.club/article/91/)

### 常见问题

- [spring是如何解决循环依赖的？](https://juejin.im/post/5c98a7b4f265da60ee12e9b2)
- [惊人！Spring5 AOP 默认使用Cglib ？从现象到源码深度分析](https://juejin.im/post/6844903982721138696)
  1. Spring 5.x 中 AOP 默认依旧使用 JDK 动态代理。
  2. SpringBoot 2.x 开始，为了解决使用 JDK 动态代理可能导致的类型转化异常而默认使用 CGLIB。
  3. 在 SpringBoot 2.x 中，如果需要默认使用 JDK 动态代理可以通过配置项`spring.aop.proxy-target-class=false`来进行修改，`proxyTargetClass`配置已无效。

## Spring Boot

- [Spring Boot 1.x基础教程](http://blog.didispace.com/spring-boot-learning-1x/)
- [Spring Boot 2.x基础教程](http://blog.didispace.com/spring-boot-learning-2x/)
- https://javadoop.com/post/spring-aop-source)

## MyBatis

### 面试

- [MyBatis 常见面试题总结](https://github.com/Snailclimb/JavaGuide/blob/master/docs/system-design/framework/mybatis/mybatis-interview.md)

# 中间件

## 注册中心

### zookeeper

- :star:[ZooKeeper 相关概念总结【入门】（Snailclimb-JavaGuide）](https://github.com/Snailclimb/JavaGuide/blob/master/docs/system-design/distributed-system/zookeeper/zookeeper-intro.md)
- :star:[ZooKeeper 相关概念总结【进阶】(Snailclimb-JavaGuide）](https://github.com/Snailclimb/JavaGuide/blob/master/docs/system-design/distributed-system/zookeeper/zookeeper-plus.md)
- :star:[ZooKeeper 实战](https://github.com/Snailclimb/JavaGuide/blob/master/docs/system-design/distributed-system/zookeeper/zookeeper-in-action.md)

## RPC框架

### Dubbo

- :star:[DUBBO原理、应用与面经总结](https://www.jianshu.com/p/292fcdcfe41e)
- [Dubbo面试题（2020最新版）](https://cloud.tencent.com/developer/article/1612348)

## 消息队列

### 总结

#### 消息队列对比

- [消息中间件部署及比较：rabbitMQ、activeMQ、zeroMQ、rocketMQ、Kafka、redis](https://juejin.im/post/6844903626171760653)

#### 笔记

1. **使用消息队列的好处**

  - **解耦**：允许我们独立的扩展或修改队列两边的处理过程；
  - **可恢复性**：即使一个处理消息的进程挂掉，加入队列中的消息仍然可以在系统恢复后被处理；
  - **缓冲**：有助于解决生产消息和消费消息的处理速度不一致的情况；
  - **削峰**：不会因为突发的超负荷的请求而完全崩溃，消息队列能够使关键组件顶住突发的访问压力；
  - **异步通信**：消息队列允许用户把消息放入队列但不立即处理它。

### Kafka

#### 基本理解

- [Kafka设计解析](http://www.jasongj.com/2015/03/10/KafkaColumn1/)
- :star::star:[Kafka技术原理](https://cshihong.github.io/2018/06/02/Kafka%E6%8A%80%E6%9C%AF%E5%8E%9F%E7%90%86/)
- :star:[Kafka架构图](https://zhuanlan.zhihu.com/p/38269875)

#### 深入理解

- :star::star:[kafka中文官网](https://kafka.apachecn.org/)
- [kafka客户端和服务端开发(三)](https://www.cnblogs.com/rickiyang/p/11074194.html)
- [kafka同步异步消费和消息的偏移量（四](https://www.cnblogs.com/rickiyang/p/11074193.html)

#### 面试

- [八年面试生涯，整理了一套Kafka面试题](https://juejin.im/post/6844903889003610119)

#### 总结

1. ZooKeeper 主要为 Kafka 提供 Broker 和 Topic 的注册以及多个 Partition 的负载均衡等功能。
2. 在 Kafka 0.9 版本之前消费者偏移量默认被保存在 zookeeper 中，但在 0.9 版本开始 consumer 将位移提交到 Kafka 的一个内部topic（该topic默认有 50 个分区，每个分区 3 个副本）。


### QMQ

去哪儿和携程内部使用的消息队列

- :star::star:[《去哪儿网消息队列设计与实现》](https://www.infoq.cn/article/b4VPvP3m8DA-PM7ZqMGZ?from=timeline&isappinstalled=0)

# 搜索引擎

## ElasticSearch

参考[es.md](https://github.com/LJWLgl/backend-study/blob/master/es.md)

# 配置中心

# 数据库

## Mysql

### 概述

- [Mysql](https://github.com/CyC2018/CS-Notes/blob/master/notes/MySQL.md)

### 索引

- :star:[数据库索引](https://github.com/Snailclimb/JavaGuide/blob/master/docs/database/%E6%95%B0%E6%8D%AE%E5%BA%93%E7%B4%A2%E5%BC%95.md)
- [Mysql B+树学习](https://juejin.im/post/59bf5cf65188252f92381fe5)
- [为什么MySQL数据库索引选择使用B+树？](https://blog.csdn.net/xlgen157387/article/details/79450295)

#### 聚簇索引和非聚簇索引

- [MYSQL索引：对聚簇索引和非聚簇索引的认识](https://blog.csdn.net/alexdamiao/article/details/51934917)

### 锁和事务

- [事务的ACID和四个隔离级别](https://www.jianshu.com/p/b1fbf903f5a0)
- :star:[MySQL innodb中各种SQL语句加锁分析](https://www.cnblogs.com/DataArt/p/10168106.html)

- [MySQL/InnoDB中，乐观锁、悲观锁、共享锁、排它锁、行锁、表锁、死锁概念的理解](https://www.souyunku.com/2018/07/30/mysql/)

- [MySQL 表锁和行锁机制](https://juejin.im/entry/5a55c7976fb9a01cba42786f)

### 主从同步

- [Mysql主从同步的原理](https://segmentfault.com/a/1190000008663001)

### 查询优化

- [常见mysql的慢查询优化方式](https://cloud.tencent.com/developer/article/1545163)

## 总结

### 笔记



## Redis

- [Redis](https://github.com/CyC2018/CS-Notes/blob/master/notes/Redis.md#%E5%85%AD%E9%94%AE%E7%9A%84%E8%BF%87%E6%9C%9F%E6%97%B6%E9%97%B4)
- [https://mrdear.cn/2018/08/19/middleware/redis--study_guide/](https://mrdear.cn/2018/08/19/middleware/redis--study_guide/)
- [Redis设计与实现](https://redisbook.readthedocs.io/en/latest/index.html)

## HBase

- [《Hbase 技术细节笔记（上）》](https://cloud.tencent.com/developer/article/1006043)
- [《Hbase 技术细节笔记（下）》](https://cloud.tencent.com/developer/article/1006044)
- [《Hbase RowKey设计》](https://juejin.im/entry/5764f4c95bbb500063f949f9)
  - rowkey 按照字典顺序排列，便于批量扫描。
  - 通过散列可以避免热点。
- [《HBase性能优化方法总结》](http://dxer.github.io/2016/04/01/hbase-optimize/)

# 分布式设计

## 负载均衡

### 算法

#### 轮询与一致性HASH

- :star:[负载均衡之随机、轮询、一致性哈希](https://www.cnblogs.com/Stephanie-boke/p/12289732.html)

## 分布式锁

- [基于redis的分布式锁实现](https://juejin.im/entry/5a502ac2518825732b19a595)

## 分布式限流

- [微服务-高并发下接口如何做到优雅的限流](https://blog.csdn.net/qq_44868502/article/details/104998125)

  限流算法：

  - **计数器限流**：

    **原理**：计数器限流的本质是单位时间内，访问量到达设置的限制后，在这个时间段没有过去之前，超过阈值的访问量拒绝处理。

    **缺点**：限流容易造成热点，某个时间段内（非单位时间内）来看会超过阈值

  - **令牌桶限流**

    **原理**：每隔一定的时间往桶内放入固定数量的定牌，当请求到来时去容器内先获取令牌，拿到了，开始处理，拿不到拒绝处理或者短暂的等待

  - **漏斗限流**

## 稳定性 & 高可用

### CAP与BASE

- [谈谈 ACID、CAP 和 BASE](http://guleilab.com/2019/05/05/acid-cap-base/)

## 服务治理

## 分布式一致

- :star::star:[分布式](https://github.com/CyC2018/CS-Notes/blob/master/notes/%E5%88%86%E5%B8%83%E5%BC%8F.md)

# 思想设计

## 微服务设计

- [微服务的4个设计原则和19个解决方案](https://www.cnblogs.com/stulzq/p/8573828.html)
  微服务的4个设计原则：
  - AKF拆分原则
  - 前后端分离
  - 无状态服务
  - Restful通信风格

## 领域模型

[阿里盒马领域驱动设计实践](https://www.infoq.cn/article/alibaba-freshhema-ddd-practice)

# 错误排查

## Http Client

- [[踩坑总结] HttpClient默认重试策略不处理SocketTimeoutException](https://juejin.im/entry/5ad0b1116fb9a028c14ae238)

# Review

- :star::star:[《写在19年初的后端社招面试经历(两年经验): 蚂蚁 头条 PingCAP》](https://juejin.im/entry/5c5122fce51d4506093462f6)
- [《Java面试通关要点汇总集》](https://juejin.im/post/5a94a8ca6fb9a0635c049e67)
- [《Java Web架构知识整理——记一次阿里面试经历》](https://juejin.im/post/5a45ff4b6fb9a0451b04e052)
- [《蚂蚁金服面试题及答案之一面（持续更新）》](https://juejin.im/entry/5c8a08b56fb9a049bb7d354d)
- [一个学渣的阿里之路](https://juejin.im/post/5b2c3a6ef265da597e35a53c)

# 推荐书籍

## Java

- 《深入理解 Java 虚拟机》

## Spring

### Spring Boot

- [《Spring MVC 到 Spring Boot 的简化之路》](https://juejin.im/post/5aa22d1f51882555677e2492)

## 代码风格

- 《clean code》

## 中间件相关

- 《Redis设计与实现》

# 面试

## P6阶段

- [最新美团Java面试题目（共3面）](https://youzhixueyuan.com/meituan-senior-java-interview-questions.html)

# 个人成长

- [如何成为一位「不那么差」的程序员](https://juejin.im/post/5b70cdf6e51d456665220632#heading-19)

# 资料整理

* [architecture.of.internet-product 互联网公司技术架构，微信/淘宝/微博/腾讯/阿里/美团点评/百度/Google/Facebook/Amazon/eBay的架构](https://github.com/davideuler/architecture.of.internet-product)
* :star::star:📚 [CyC Computer Science Learning Notes (技术面试需要掌握的基础知识整理)](https://github.com/CyC2018/CS-Notes)
* [😮 advanced-java 互联网 Java 工程师进阶知识完全扫盲](https://github.com/doocs/advanced-java)
* [technology-talk 汇总java生态圈常用技术框架、开源中间件，系统架构、项目管理、经典架构案例、数据库、常用三方库、线上运维等知识](https://github.com/aalansehaiyang/technology-talk)
* [architect-awesome 《后端架构师技术图谱》](https://github.com/xingshaocheng/architect-awesome)
* [To Be Top Javaer - Java工程师成神之路](https://github.com/hollischuang/toBeTopJavaer)
* [miaosha 😮😮秒杀系统设计与实现.互联网工程师进阶与分析🙋🐓](https://github.com/qiurunze123/miaosha)
* [interviews 软件工程技术面试个人指南](https://github.com/kdn251/interviews/blob/master/README-zh-cn.md)
* [JavaGuide 【Java学习+面试指南】 一份涵盖大部分Java程序员所需要掌握的核心知识](https://github.com/Snailclimb/JavaGuide)
* [🎓 Java Core Sprout : basic, concurrent, algorithm](https://github.com/crossoverJie/JCSprout)
* [j360-tools Java底层知识点、技术栈相关原理知识点、工具最佳实践](https://github.com/xuminwlt/j360-tools)
* [java-knowledge-mind-map](java-knowledge-mind-map)
* [technology-talk汇总java生态圈常用技术框架](https://github.com/aalansehaiyang/technology-talk)
* [JCSprout](https://github.com/crossoverJie)

- [3y](https://github.com/ZhongFuCheng3y/3y/)