## 事务（来自刘驰总结）

--查看隔离级别
    select  @@global.tx_isolation, @@tx_isolation;

--修改隔离级别
    set [session | global] transaction isolation level [ read uncommitted | read committed | repeatable read | serializable]

--设置全局隔离级别
    set global transaction isolation level read committed;
--设置当前会话隔离级别
    set session transaction isolation level read committed;

--开启事务
    begin；start transaction;

--禁用自动提交，每个SQL语句或者语句块所在的事务都需要显示"commit"才能提交事务
--autocommit  =  1 这种模式会在每条语句执行完毕后把它作出的修改立刻提交给数据库并使之永久化.
    set autocommit = 0；

--读锁或者写锁在事务提交时候释放
    SELECT * FROM test WHERE id = 1  LOCK IN SHARE MODE  //读锁
    SELECT * FROM test WHERE id = 1  for update  //写锁

快照读:
    select * from test where id = 1001;
快照读各种隔离级别的下的表现:
    1.读未提交:忽略
    2.读已提交:不加锁
    3.可重复读:不加锁
    4.串行化:加读锁(范围如下)
        4.1.数据存在且Mysql使用索引
            (1)id为主键: 锁一条记录
            (2)id为唯一索引:锁一条记录
            (3)id为普通索引:gap key(左开右开) +record lock
            (4)id无索引:gap key(所有gap锁) + record lock(所有记录)
    4.2. 数据不存在且使用索引
            (1)id为主键:gap锁(左开右开)
            (2)id为唯一索引:gap锁(左开右开)
            (3)id为普通索引:gap key(左开右开)
            (4)id无索引:gap key(所有gap锁) + record lock(所有记录)
    4.3. 不适用索引
            gap key(所有gap锁) + record lock(所有记录)


当前读:
    select * from test where id = 1 lock in share model(读锁)
    select * from test where id = 1 for update(写锁)
    insert test values(x,x,x,x)(写锁)
    delete from test where id = 1(写锁)
    update test set id = x where id = 1(写锁)

当前读各种隔离级别的下的表现
    1.读未提交:忽略
    2.读已提交:加锁(读已提交 只对查找出来的结果集加锁,不会加间隙锁,不保证可重复度)
        2.1.数据存在且Mysql使用索引
            (1)id为主键: 锁一条记录
            (2)id为唯一索引: 锁一条记录
            (3)id为普通索引: record lock
            (4)id无索引: record lock(所有记录)(会迅速优化成对指定记录加锁)
        2.2. 数据不存在且使用索引
            (1)id为主键:无锁
            (2)id为唯一索引:无锁
            (3)id为普通索引:无锁
            (4)id无索引:无锁
        2.3. 不适用索引
            结果集加锁
    3.可重复读:加锁
        3.1.数据存在且Mysql使用索引
            (1)id为主键: 锁一条记录
            (2)id为唯一索引:锁一条记录
            (3)id为普通索引:gap key(左开右开) +record lock
            (4)id无索引:gap key(所有gap锁) + record lock(所有记录) ----(整张表不能insert)----
        3.2. 数据不存在且使用索引
            (1)id为主键:gap锁(左开右开)
            (2)id为唯一索引:gap锁(左开右开)
            (3)id为普通索引:gap key(左开右开)
            (4)id无索引:gap key(所有gap锁) + record lock(所有记录)----(整张表不能insert)----
        3.3. 不适用索引(当索引区分度不高或者强制类型转换等导致没有索引失效,给全部记录加锁)
             gap key(所有gap锁) + record lock(所有记录)----(整张表不能insert)----
        4.串行化:加读锁(范围如下)
            4.1.数据存在且Mysql使用索引
                (1)id为主键: 锁一条记录
                (2)id为唯一索引:锁一条记录
                (3)id为普通索引:gap key(左开右开) +record lock
                (4)id无索引:gap key(所有gap锁) + record lock(所有记录)
            4.2. 数据不存在且使用索引
                (1)id为主键:gap锁(左开右开)
                (2)id为唯一索引:gap锁(左开右开)
                (3)id为普通索引:gap key(左开右开)
                (4)id无索引:gap key(所有gap锁) + record lock(所有记录)
            4.3. 不适用索引
                 gap key(所有gap锁) + record lock(所有记录)

意向锁与实际加锁:
    可重复度隔离级别下,两个线程可以同时对不存在的数据加锁,且都能成功,都加锁后,任一个线程插入会等待,若另一个线程也插入,则会死锁

RR隔离级别下数据分布
| id  | b    | c    | d    |
+-----+------+------+------+
|   1 |    1 |    1 |    1 |
|  10 |   10 |   10 |   10 |
|  50 |   50 |   50 |   50 |
| 100 |  100 |  100 |  100 |
a									b
begin;								begin;
									insert test values(75,75,75,75);
									Query OK, 1 row affected (0.00 sec)
insert test values(76,76,76,76);
Query OK, 1 row affected (0.00 sec)
insert test values(74,74,74,74);
Query OK, 1 row affected (0.00 sec)	
insert test values(75,74,74,74);
等待
---------insert锁住最小范围id=75的记录--

Mysql RR下幻读:
     T1:                                                T2
     begin;                                             begin;
     select * from test where id = 1;(empty list)       insert test values(1,10);(success)
                                                        commit;
     insert test values(1,10);(error)

spring的事务处理
1.七种事务传播特性
    Required:需要事务环境。若上下文存在事务环境则支持，否则新建事务
    RequirsNew:需要新的事务环境。重新获取新的连接，开启新的事务
    Supports:支持当前事务，如不存在则普通运行，不开启事务
    NotSupported:以非事务状态运行
    Mandatory:必须存在事务环境，否则抛出异常
    Never:必须不存在事务环境，否侧抛出异常
    Nested:事务嵌套。sql的savepoint机制，内部回滚外部不回滚
2.事务生效：
    必须使用spring的代理对象，如autowired注入或者AopContext获取到的代理。
    直接在非事务方法调用事务方法，事务不生效
3.事务提交或者回滚
    @Transactional(propagation = Propagation.REQUIRED)
    public void insrt() {
        success();
        try {
            service2.fail();//另一个类的事务方法
        } catch (Exception e) {}//捕获该异常，观察该方法的事务是否会回滚
        success();//p2
    }
    结论：service2.fail()只有开启新的事务或者以非事务运行,insrt才会提交（REQUIRES_NEW  NOT_SUPPORTED NESTED,以及不写@Transaction）
         其他形式会导致insrt才会回滚，因为在事务上下文已经标记该事务要回滚了。代理会执行到p2,但上层使用者收到异常
4.Propagation.NOT_SUPPORTED 与 没有@Transactional区别
   没有@Transactional,会被当做外层事务的一部分
   Propagation.NOT_SUPPORTED,会与外层事务隔离