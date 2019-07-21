## 事务的ACD性质
1. 原子性（Atomicity）
2. 一致性（Consistency）
3. 隔离性（Isolation）
4. 持久性（Durability）
### 隔离性的4个级别
**读未提交（Read Uncommitted）**
读未提交的实现：`读锁、写锁都在一个原子操作（如select、insert等）完成后立即释放。`换句话说，事务作出更新后，不管是否提交，由于已经释放了目标记录的写锁，更新对其他事务就是可见的。
** 读已提交（Read Committed）**
出现脏读的原因是写锁的持有时间过短。读已提交针对这一问题作出了优化：读锁仍然在一个原子操作完成后立即释放；写锁从写操作开始持有，事务提交后释放。事务作出更新前，会先申请目标记录的写锁，并持续持有至事务提交后，释放锁后，更新对其他事务才是可见的。
**可重复读（Repeatable Read）**
解决不可重复读可以使用两种方法：
悲观策略：串行化
乐观策略：多版本 + 冲突检测
**可序列化（Serializable）**
幻读是一种特殊的不可重复读。

```table
隔离级别/问题 |	脏读 | 不可重复读 | 幻读
读未提交	 | Y | Y | Y
读已提交	 | - | Y | Y
可重复读	 | - | - | Y
可序列化	 | - | - | -
```
## 主从同步原理
###