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
## 2019.7携程IBU（国际事业部）
### 一面
- 线程池`submit()`与`execute()`区别
- 线程池有哪几种缓冲队列？`LinkedBlockingQueue`和`ArrayBlockingQueue`的区别？
- `@Component`与`@Configuration`注解的区别？
- 描述一下Spring Boot启动原理
-  Spring boot中jar包与war包区别？
    - [https://www.cnblogs.com/cag2050/p/7833541.html](https://www.cnblogs.com/cag2050/p/7833541.html)
- 是否阅读过Flink源码？
- linux中拷贝命令是哪一个？
### 二面
- SQL慢查询如何定位和优化
- 发起
- 线程池如何配置？是否配置过拒绝策略
### 三面
- 堆排序如何实现
- Spring事务实现原理
- Redis跳跃表的实现
### HR
### 2019.7大搜车一面



