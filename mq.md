##QMQ
QMQ是去哪儿自己设计和实现一款消息队列，该消息队列能够保证一致性，具备较高吞吐量，支持消息延迟发送，已在携程、便利蜂等公司中广泛使用。
### 客户端一致性
QMQ通过mysql事务实现客户端一致性，当调用`sendMessage`方法，执行时会分为两步：
1. 向`message DB`中先插入一条message
2. 开启事务 -> 真正发送message到Server -> 删除之前在messageDB中的记录 -> 提交事务
如果message发送到Server失败，DB中的记录就不会被删除，后面会有Task重新执行发送逻辑，伪代码如下
```java
@Transactional
public void pay(Order order){
    PayTransaction t = buildPayTransaction(order);
    payDao.append(t);
    //producer.sendMessage(buildMessage(t));
    final Message message = buildMessage(t);
    messageDao.insert(message);
    // 在事务提交后执行
    triggerAfterTransactionCommit(()->{
        messageClient.send(message);
        messageDao.delete(message);
    });
}
```
### 存储模型