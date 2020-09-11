# 知识点脑图
<div align="center"> <img src="http://tc.ganzhiqiang.wang/java-review-knowlege.png"><p>Java知识点脑图</p> </div><br/>
# 2019
## 2019.6 拼多多——AI引擎方向
### 一面
面试基本上都围绕项目，特别是笔者用Flink做的用户实时推荐。。。
**笔试题**
1)  求n的平方根（向下取整，禁止用函数）
比较简单就不贴代码了，考虑效率问题，可以用二分查找来实现
2） g(x)函数输出1、2、3、4、5的概率都是1/5，现在要求p(x)函数使用g(x)函数，使p(x)输出1、2、3的概率都是1/3


这种题目都不难，只要抓住面试官想考察的重点即可，就这道题来说，不必理会具体的概率，只要p(x)调用g(x)获取到4或者5，就再次调g(x)重试，直到输出结果是1、2、3，伪代码如下：
```java
int a(x)  {
    int x = g(x);
    whiile (x > 3) {
        x = g(x)
    }
    return x;
}
```
### 二面
**面试题**
面试同样是问Flink项目，项目背景、项目流程、存入redis如何优化，
**笔试题**
1) 自己实现一个队列，包含push和pop方法
笔者先用单链表实现了一个，pop的时候需要遍历链表，效率较低，后来在面试中又改进了一版，加了tail节点，并采用双向链表实现，保证pop的复杂度为O(1)，伪代码如下：
```java
public T pop() {
    T value = tail.value;
    Node preNode = tail.pre;
    tail = preNode;
    preNode.next = null;
    reyutn value;
}
```
做完之后，面试官没说什么，只是让我等一下，然后 and 然后。。。，HR就来了，然后就被告知面试未通过，说技术栈不符合他们的要求，真是一脸懵逼啊（不符合你们技术栈，还让我来面试。。）
### 总结
拼多多给笔者感觉太注重业务，也可能是技术栈不符合人家要求，人家也不知道怎么问（手动狗头）
## 2019.7携程IBU——国际事业部
### 一面
- 线程池`submit()`与`execute()`区别
- 线程池有哪几种缓冲队列？`LinkedBlockingQueue`和`ArrayBlockingQueue`的区别？
- `@Component`与`@Configuration`注解的区别？
- 描述一下Spring Boot启动原理
-  Spring boot中jar包与war包区别？
    - [https://www.cnblogs.com/cag2050/p/7833541.html](https://www.cnblogs.com/cag2050/p/7833541.html)
- 是否阅读过Flink源码？
- linux中拷贝命令是哪一个？
- spring security包含哪些拦截器？
- Rocketmq和qmq(去哪儿开源的消息队列)的区别？
### 二面
- SQL慢查询如何定位和优化？
- HttpClient发起update请求（无返回值），是否要关闭reponse
- 线程池如何配置？是否配置过拒绝策略
- HBase做了哪些写入优化？
### 三面
- 堆排序如何实现
- Spring事务实现原理
- Redis跳跃表的实现
### HR
- 离职原因
- ...
## 2019.7 秦苍（买单侠）
## 一面
一面基本上没问什么，直接略过了...，没事多写写sql，比如最不常用instert、delete语句，小心在sql上翻车
## 二面
面试过程中真的一直在抛问题，很多问题都是点到为止，没有深入
- mysql未命中索引的情况？
- 编译时异常和运行时异常的区别？
    - 参考链接：[Java运行时异常和非运行时异常](https://blog.csdn.net/huhui_cs/article/details/38817791)
- 懒汉模式的实现的几种方式？
    - 双重锁
- 建立联合索引和建立多个单个索引哪个更好？
    - 答：建立联合索引更好，因为索引建立的越多占用的磁盘空间越多，更新数据时会更慢
- 知道CAP理论吗?`zookeeper`和`Euraka`各自保证CAP中的哪些？
    - 答：C：一致性，A：可用性，P：分区容错性，P一定是要保证的，其中ZK保证CP，`Euraka`保证AP和弱一致性
- 能举一个最终一致性的例子吗？
## 三面
三面是个技术负责人，估计是看我薪资要高了，来考察考察我的水平
- 详细描述一下Redis的zset以及内部如何实现的？
    - 答：zset是个有序表，使用了`压缩链表`或者`跳跃表`来实现，后面和他讲了跳跃表的逻辑
- 对架构的理解？架构师应该做哪些事？
- 设计模式遵循哪些原则？怎么理解`开闭原则`？`

三轮面试总共面了4个小时...

## 2019.7 有赞——有赞云
### 一面
- 先问了项目经验？比如clog如何实现？
- 有没有使用过分布式锁，是自己实现的吗？应用场景在哪？
- 谈谈你对`可重入锁`的理解？为什么称为`可重入`？
- `ConcurrentHashMap`内部实现？
听说有赞云类似有赞的中间件部门，主要提供基础组件的，但是很可惜笔者只面了一面，后面有机会也想这个团队有多NB
## 2019.7 丁香园（杭州）

- 谈谈你对`可重入锁`的理解？为什么称为`可重入`？

## 2019.7 大搜车（杭州）
大搜车是一家阿里系的公司，职级也是和阿里靠近的，主要做金融车贷，之前获得阿里几亿的融资，在杭州也算较大的互联网公司，笔者感觉还是不错的，可是知友好像对它有偏见，评价不是很好~
### 一面（电话面试）
- 有没有使用设计模式
### 二面
- Mysql有哪几种情况没有命中索引？像这种`where age = 5 + 1`会命中索引吗？
    - 索引字段参与运算的才不会命中索引，如`where age + 10 = 30`，上面的列子是可以命中索引的
- Mysql未命中索引会导致哪些问题？那全表扫描会导致哪些问题？
    - 答：有可能导致磁盘IO过高，另外，全表扫描会锁整个表，其他事务不能执行
- Spring事务的传播机制包含哪些？
- http header指定哪些参数可以优化性能？
    - 可以从`Cache-Control `介绍
- 你是怎么理解DDD（领域驱动）的？
    - 重点讲了充血模型
- 双亲委派中，为什么交由父加载器加载，如何防止重复加载？
- ThreadLocal使用过吗？它在使用中应该注意什么问题？
    - 答：使用结束需要remove，防止内存泄露
- 设计模式中六大设计原则有哪些？怎么理解开闭原则?
- 代码中包含大量的if-else语句，该使用哪种设计模式优化？
    - 答：策略模式
笔者对二面面试官印象不错，比较会引导候选人逐渐深入问题，后来知道他是从阿里出来的，果然是牛逼啊，最后给了我P5+
## 2019.7.22 酷家乐（杭州）
- Redis为什么这么快？
    - 基于内存，基于NIO的多路复用
- 跳跃表的查询复杂度？
    - 插入和查找都是O(logN)）
- Redis如何防止雪崩的问题？
- 你用过哪些JUC下面的工具类？
- JVM有哪些分区
- 垃圾回收算法有哪些？你们服务器用的什么垃圾回收器？
- 有JVM调优的经验吗？
## 2019.7.27 口碑
### 一面
- 堆排序的过程？
- `select * from user where age > =20 and age  < 30 order by name`这个sql语句的执行流程如何？排序是在哪里做的？
- mysql事务隔离级别中，`读已提交`和`可重复读`的区别是什么？
- 了解mysql中的`间隙锁`吗？
- 【场景题】A用户转账给B用户如何保证一致性？
    - 答：用延迟消息去check
- 【场景题】两步操作，一步是本地DB，一步是RPC，如何保证原子性？
- 你还有什么想问我的？

## 总结

- [x] 大搜车

- [x] 携程

- [ ] 拼多多

- [ ] 口碑

  


