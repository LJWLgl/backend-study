## 收到offer及意向offer

- [ ] 途虎养车（搜索方向）
- [ ] 比心（Java方向）
- [x] 喜马拉雅（搜索方向）
- [ ] B站（搜索方向，C++技术栈）
- [x] OYO（搜索方向）
- [ ] 小红书（搜索方向，Go技术栈）
- [x] 得物 （搜索方向）
- [x] 美团（聊offer中，Java-Tars系统）
- [x] 阿里（聊offer中，Java-直播）

## 2020.8.31 阿里飞猪（搜索方向）

### 一面

1. 问了项目，如何重构结果页的，怎么把时间缩短到200ms？
2. Spring Boot与Spring MVC区别？
3. 有A和B两个有序数组，A的长度是l，A的元素和B的元素的个数分别是m和n，已知l > m+n，如何将A和B合并一个有序数组？
4. 有笔试题，单独约了笔试时间，题目不难，两道题在leecode上都有原题。(详细参考：data/20200904-alifeizhu.txt)
   - 给定两个二叉树，编写一个函数来检验它们是否相同
   - 给定字符串（合法字符只包括0，1，？），替换字符串中的通配符？为0或者1，生成所有可能的字符串。比如输入的字符串为"1??0?101"

### 二面
1. es选举master的过程
2. **es亿级数据量的查询如何优化？**
3. es部署如何优化？可以设置哪些调优参数？
4. kafka是拉模式还是模式？内部原理有了解过吗？你们为什么用qmq不用kafka ?
5. 笔试题：链表A,链表B,找对应的重复元素

### 三面
1. jvm内存如何分区？垃圾回收算法？g1的优势是什么？
2. JVM的-Xss、-Xmn、-XX:PretenureSizeThreshold、-XX:MaxTenuringThreshold 这些参数是什么意思？
3. 线程池有哪些核心参数？核心线程数一般怎么定义？
4. mysql的having和where的区别？
5. 怎么理解AOP和IOC的？spring是如何实现aop的？除了Spring，用过其它似框架吗？
6. 有什么想问我的？

### HR
1. 自我介绍
2. 工作内容
3. 工作最有挑战的事
4. 目前薪资

## 2020.9.1 途虎养车网（搜索方向）
### 一面
1. 你们刷新数据有几种方式？
   答：途虎是每天新建索引，将Alias指向新的索引，个人觉得数据量较小可以这么做，也可以解决脏数据的问题
2. 你们是怎么做ES分词的？
   答：途虎是事先分词后，再索引到es，然后用空格分词
3. 你们是如何解决es脏数据的问题？
4. java锁如何实现，比如sycnizered
   答：原理的是JDK的动态代理
5. hashmap是如何实现的
6. 你们是如何使用jdk8实现异步的
7. Java注解的实现原理

## 2020.9.11 喜马拉雅（搜索方向）
### 一面

1. 你知道es和solr的区别吗？
   - 为什么solr查询是比es快的？
   - 为什么es写入比solr稳定？
2. lucene底层的update和add是如何实现的？
3. es常用的聚合操作有哪些？district和group，底层原理是怎么做的？
4. es如何实现深分页？
5. 平衡二叉树和跳跃表是如何实现的？

### 二面 

1. 

### 三面

1. 

### HR

表示是我见过最狠的HR，各种压力测试

1. **和别的候选人比，你的优点在哪里**

总结：可惜了，喜马拉雅还不错的公司，可是薪资没给到位（涨幅20%），最后拒了offer


## 2020.10.19 OYO（搜索方向）

### 一面

1. 线程池有哪些哪几个核心参数？分别是哪5个？随着请求量的增多线程数是怎么创建的？了解过SynchronousQueue吗？	

   注意：

   - 当有任务来时，java线程池会把任务先放进缓存队列，然后线程池从队列里获取任务创建线程；
   - *Executors*.*newCachedThreadPool*()用的就是**SynchronousQueue**，所以能无限创建

   参考：[Java线程池中SynchronousQueue、LinkedBlockingQueue和ArrayBlockingQueue](https://xmcf.me/?p=346)

2. 写个单例模式吧？volatile如何防止指令重排?

   答：volatile通过cpu的内存屏障

3. MySQL什么是聚簇索引和非聚簇索引？最左匹配原则？

4. 你们怎么用本地缓存和redis的？针对请求量过大的场景？

   答：先用本地缓存再用Redis

### 二面

### 三面

### HR

## 2020.10.19 小红书（搜索方向）
小红书的搜索分为三个流程，召回、排序、工程，我面试的是工程方向，技术栈主要是go
### 面试评估（电话）
主要问了大搜的项目经验、集群配置、数据量等
### 一面（是）

## 2020.10.26得物（搜索工程-Java开发）
### 一面

1. es的master选举
2. 

### 二面
### 三面
### 四面

1. 

### HR

## 2020.10.23 阿里企业智能事业部（Java-直播方向）
### 面试评估

- ES

### 一面
### 二面
### 三面
### 业务HR
### HRBP

## 2020.10.28 美团（Java-工程效率tars系统）
### 一面
1. 数组倒排，时间复杂度为1
### 二面
1. jwt token 
### HRBP

1. 什么样的岗位是你会考虑的？