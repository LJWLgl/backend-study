## 存储引擎

### InnoDB

### MyISAM

### MyISAM与InnoDB区别

1. **是否支持行级锁** : MyISAM 只有表级锁(table-level locking)，而InnoDB 支持行级锁(row-level locking)和表级锁,默认为行级锁。
2. **是否支持事务和崩溃后的安全恢复： MyISAM** 强调的是性能，每次查询具有原子性,其执行速度比InnoDB类型更快，但是不提供事务支持。但是**InnoDB** 提供事务支持，外部键等高级数据库功能。 具有事务(commit)、回滚(rollback)和崩溃修复能力(crash recovery capabilities)的事务安全(transaction-safe (ACID compliant))型表。
3. **是否支持外键：** MyISAM不支持，而InnoDB支持。
4. **是否支持MVCC** ：仅 InnoDB 支持。应对高并发事务, MVCC比单纯的加锁更高效;MVCC只在 `READ COMMITTED` 和 `REPEATABLE READ` 两个隔离级别下工作;MVCC可以使用 乐观(optimistic)锁 和 悲观(pessimistic)锁来实现;各数据库中MVCC实现并不统一。推荐阅读：[MySQL-InnoDB-MVCC多版本并发控制](https://segmentfault.com/a/1190000012650596)

## 事务

### ACID
- **原子性（Atomicity）**：一个事务必须被视为一个不可分割的最小工作单元，整个事务中的所有操作要么全部提交成功，要么全部失败回滚，对于一个事务来说，不可能只执行其中的一部分操作。
- **一致性（Consistency）**：数据库总是从一个一致性的状态转换到另一个一致性的状态。
- **隔离性（Isolation）**：通常来说，一个事务所做的修改在最终提交以前，对其他事务是不可见的。针对不同的业务需求，**隔离性**分为4个级别：读未提交、读已提交、可重复读、串行化。
- **持久性（Durability）**：通常来说，一旦事务提交，则其所做的修改会永久保存到数据库（即使系统崩溃，修改的数据也不会丢失）。针对不同的业务需求，持久性也分为多个级别，此处略。

- 幻读是指在同一事务下，连续执行两次同样的SQL语句，第二次的SQL语句可能会返回之前不存在的行。

### 隔离级别

隔离级别/问题 |	脏读 | 不可重复读 | 幻读
--- | --- | --- | ---
读未提交（Read Uncommitted）	 | Y | Y | Y
读已提交（Read Committed）	 | - | Y | Y
可重复读（Repeatable Read）	 | - | - | - 
可序列化（Nonrepeatble Read）	 | - | - | -

## 锁

- 页锁
- 表锁
	- 意向锁
    意向锁的主要目的是显示事务正在锁定某行或者正意图锁定某行，事务要获取某个表上的S锁和X锁之前，必须先分别获取对应的IS锁和IX锁
    - 意向排它锁（IX锁）
    - 意向共享锁（IS锁）
- 行锁
  - 读锁（S锁，又称共享锁）
  - 写锁（X锁，又称排它锁）
- gap锁（间隙锁）
    间隙锁作用在索引记录之间的间隔，又或者作用在第一个索引之前，最后一个索引之后的间隙。不包括索引本身。一般在当前读RR使用gap锁，防止幻读问题。
- Next-key锁
Next-key锁实际上是Record锁和gap锁的组合。Next-key锁是在下一个索引记录本身和索引之前的gap加上S锁或是X锁(如果是读就加上S锁，如果是写就加X锁)。 

**参考**

- [MySQL/InnoDB中，乐观锁、悲观锁、共享锁、排它锁、行锁、表锁、死锁概念的理解](https://cloud.tencent.com/developer/article/1523026)
- [抱歉，没早点把这么全面的InnoDB锁机制发给你](https://dbaplus.cn/news-11-2518-1.html)
- [MySQL 的加锁处理，你都了解的一清二楚了吗？（来自何登成的博客）](https://zhuanlan.zhihu.com/p/144471126)
- [MySQL锁机制——你想知道的都在这！](https://juejin.im/post/6844903901871734792#heading-21)
- [Innodb锁机制：Next-Key Lock 浅谈](https://www.cnblogs.com/zhoujinyi/p/3435982.html)

## 索引

### 聚簇索引

### 非聚簇索引

### 哪些情况下不能使用索引（explain解释type为ALL）

1. 不符合最左匹配原则。

   ```sql
   # id,name,age为联合索引
   最左匹配索引
   > select id,name,age from user where name = 'xm'
   ```

2. like查询是以%号开头，不会使用索引。

3. where子句对索引上有数学运算或者使用函数，不会使用索引。

   ```sql
   # 不会使用索引
   > select * from user where id + 1 = 1000
   # 注意下面sql会使用索引
   > select * from user where id = 1000 + 1
   # 不会使用索引
   > select * from user where pow(id,2) = 1000;
   ```

4. 存在索引列的数据类型隐形转换，不会使用索引

   ```sql
   # name为字符串类型，下面据类型隐形转换，所以不会使用索引，123需要使用引号（'123'）
   > select * from user where name = 123
   ```
5. mysql执行计划认为不使用索引查询会更快，也不会使用索引。

**参考**

- [MYSQL 索引类型、什么情况下用不上索引、什么情况下不推荐使用索引](https://blog.csdn.net/kaka1121/article/details/53395628)

## 常见问题

1. 一条sql查询很慢，有可能是哪些原因导致？

   偶尔很慢可能是以下原因：

   - 数据库在刷新脏页，例如 redo log 写满了需要同步到磁盘。
   - 执行的时候，遇到锁，如表锁、行锁。

   一直很慢可能是以下原因：

   - 没有用上索引：例如该字段没有索引；由于对字段进行运算、函数操作导致无法用索引（可参考上文）。
   - 数据库选错了索引。

   参考：

   - [腾讯面试：一条SQL语句执行得很慢的原因有哪些？](https://mp.weixin.qq.com/s?__biz=Mzg2OTA0Njk0OA==&mid=2247485185&idx=1&sn=66ef08b4ab6af5757792223a83fc0d45&chksm=cea248caf9d5c1dc72ec8a281ec16aa3ec3e8066dbb252e27362438a26c33fbe842b0e0adf47&token=79317275&lang=zh_CN#rd)
   
2. mysql有哪些情况会导致死锁？如何避免死锁？

   如图所示：

   ![img](https://pic3.zhimg.com/80/v2-5d48639658d0fdbd8f32cdd45742cde6_1440w.jpg)

   非常好理解，也是最常见的死锁，每个事务执行两条SQL，分别持有了一把锁，然后加另一把锁，产生死锁。

   **避免死锁**

   - 保证两个session加锁顺序是一致的
