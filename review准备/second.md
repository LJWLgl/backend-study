# XC

**目标：45w（year）**

|         | 16        | 15        | 14        | 13       |
| ------- | --------- | --------- | --------- | -------- |
| Monthly | 27k ~ 28k | 29k ~ 30k | 31k ~ 32k | 33 ~ 34k |
| pdd     | 30k       |           |           |          |
| alibaba | 28k       |           |           |          |

# RV

### 自我介绍

我叫甘志强，本科毕业安徽师范大学，专业是软件工程，是18年校招到途家网，做的是Java开发，后面转岗到携程国际研发部的搜索团队，入职后一直在维护trip.com的大搜，目前有两年多工作经验，一年多的搜索相关经验，期间也接触到部分nlp相关的知识。

### 自定义插件的相关问题

1. 为什么要自定义开发es插件
答：原因有以下几点
- 产品希望能支持自定义的专业词库，现在用日语词库，都是我们自己整理的
- es自带的kuromoji插件分词效果不是很好
2. 开发lucene插件核心类是什么？

   答：Analyzer类和TokenStream类型

3. 在开发自定义有遇到问题吗？
   答：

## es相关题

### es基础

1. Lucene、solr以及elasticsearch之间的区别

   答：区别和联系主要如下：

   首先他们的联系是：

   - 两者都是基于lucene开发

   区别：

   - 分布式这块，solr/solrCloud借助zookpper实现，而Elasticsearch自己实现了分布式协调管理（组件xen）
   - 全文搜索方面solr搜索是比es快的，但是es支持近实时搜索，而solr不支持
   - 当实时建立索引时，Solr 会产生 io 阻塞，查询性能较差，Elasticsearch 具有明显的优势。随着数据量的增加，Solr 的搜索效率会变得更低，而 Elasticsearch 却没有明显的变化。
   - 在聚合查询，比如distinct、group等，es表现更好；
   - 在运维方面，es提供了多个api，非常便于维护；

   参考：

   - [为什么我们要选用 Elasticsearch 而不用 Solr](https://learnku.com/articles/43880)

   - https://cloud.tencent.com/developer/article/1184361

2. es有哪些常用的参数配置？

   答：es常用配置如下，配置文件为%ES_HOME%/config/elasticsearch.yml

   **JVM**

   - -Xms31g -Xmx31g

     堆的最大最小内存一般是机器内存的一半，不要超过32G。如果使用`Doc Vlaue`，则jvm可以设置的更小（4G~32G），便于将`Doc Vlaue`缓存到内存。

   - Lucene内存

     剩下的一半给Lucene，用于缓存segements文件，加速文件检索

   **Memory内存配置**

   - :white_check_mark:bootstrap.memory_lock: 是否锁住内存，避免交换(swapped)带来的性能损失,默认值是: false:

   - :white_check_mark:indices.fielddata.cache.size（节点用于 fielddata 的最大内存）

     如果 fielddata达到该阈值，就会把旧数据交换出去。该参数可以设置百分比或者绝对值。默认设置是不限制，所以强烈建议设置该值，比如 10%。

   - :white_check_mark:indices.breaker.fielddata.limit（ fielddata 断路器的触发值）
     fielddata断路器默认设置堆的 60% 作为 fielddata 大小的上限。

   - indices.breaker.request.limit
     request 断路器估算需要完成其他请求部分的结构大小，例如创建一个聚合桶，默认限制是堆内存的 40%。

   - indices.breaker.total.limit
     total 揉合 request 和 fielddata 断路器保证两者组合起来不会使用超过堆内存的 70%。

   **Index配置**

   - :white_check_mark:index.number_of_shards（设置索引的分片数,默认为5）

     number_of_shards是索引创建后一次生成的,后续不可更改设置

   - index.number_of_replicas（设置索引的副本数,默认为1）

   - index.refresh_interval（索引的刷新频率，默认1秒）

     该值太小会造成索引频繁刷新，新的数据写入就慢了。（此参数的设置需要在写入性能和实时搜索中取平衡）

   - cluster.routing.allocation.same_shard.host（防止同一个分片（shard）的主副本存在同一个物理机上）

   **Discovery配置**

   - :white_check_mark:discovery.zen.minimum_master_nodes（选举一个Master至少需要多少个节点，一般设置成N/2 + 1）

   参考：

   - [堆内存:大小和交换](https://www.elastic.co/guide/cn/elasticsearch/guide/current/heap-sizing.html)
- [ 限制内存使用](https://www.elastic.co/guide/cn/elasticsearch/guide/current/_limiting_memory_usage.html)
   - https://www.elastic.co/guide/en/elasticsearch/reference/current/circuit-breaker.html
- [Elasticsearch 常用配置参数总结]()
  
3. es match query（全文查询参数）有哪些参数？

   - operator：默认or，or或者and
   - minimum_should_match：operate为or下最小匹配数
   - analyzer：指定的分词器，使用mapping时指定的分词器
   - lenient：默认值是 false ， 表示用来在查询时如果数据类型不匹配且无法转换时会报错。如果设置成 true 会忽略错误。
   - fuzzniess：模糊查询时指定的编辑距离，默认为AUTO（字符串长度）
   - prefix_length：不会“模糊化”的初始字符数。这有助于减少必须检查的术语数量，默认为0
   - max_expansions：fuzzy查询将扩展到 的最大术语数。默认为50，设置小，有助于优化查询
   - transpositions：是否支持模糊转置（ab→ ba），默认是false
   - synonyms：同义词，自定义分词器的可以使用
   参考：[要搞懂 Elasticsearch Match Query，看这篇就够了](https://segmentfault.com/a/1190000017110948)

4. es如何实现聚合操作aggregation的？

   答：借助DocVlaue和FieldData实现桶和指标聚合操作

   具体查询请参考：

   - [elasticsearch系列六：聚合分析（聚合分析简介、指标聚合、桶聚合）](https://www.cnblogs.com/leeSmall/p/9215909.html)

5. Elasticsearch如何做到亿级数据查询毫秒级返回？

   答：主要从以下几方面优化

   - 冷热数据分离，建两个索引分别存放冷热数据
   - 提高节点filesystem cache大小，至少是每个数据节点的一半（比如64G内存的机器，es的jvm内存分配31G，其余的给filesystem cache即lucene）
   - 数据预热，定时任务搜索热词，保证热数据始终在在FileSystem Cache，做到毫秒级缓存
   - 调小fielddata或禁用fielddata
   - 不要做深分页，如果真的要做Scroll API，生成快照，不可跳页访问
   - 数据截取（待调研，小红书面试官提供的方案，大概意思是查到符合条件的N条件记录后就返回，不需要查后面的数据）
   - 可以直接查询主分片，省去路由时间

   详细参考：https://cloud.tencent.com/developer/article/1446107

6. es如何实现深度翻页？

   - [ElasticSearch如何支持深度分页](http://arganzheng.life/deep-pagination-in-elasticsearch.html)

7. 说一下es的分布式架构原理 / es是如何实现分布式的

   答：es分布式的核心在于在多个机器上启动多个es实例，组成es集群。一个index（索引）会包含多个分片，每个分片都是一个最小工作单元，每个分片存储部分数据，每个主分片又有主分片和副分片，主分片接收读写请求，而副分片只接收读请求，承担读负载。

   参考：https://mp.weixin.qq.com/s/3D6ikLDrPHpKsU6RSz012Q（第一点）

8. 说一下es的写入数据流程以及底层原理

   答： primary shard（主分片内部流程如下） 

   Primary请求的入口是PrimaryOperationTransportHandler的MessageReceived, 当接收到请求时，执行的逻辑如下

   1. **判断操作类型** 遍历bulk请求中的各子请求，根据不同的操作类型跳转到不同的处理逻辑
   2. 将update操作转换为Index和Delete操作 获取文档的当前内容，与update内容合并生成新文档，然后将update请求转换成index请求，此处文档设置一个version v1
   3. **Parse Doc** 解析文档的各字段，并添加如_uid等ES相关的一些系统字段
   4. **更新mapping** 对于新增字段会根据dynamic mapping或dynamic template生成对应的mapping，如果mapping中有dynamic mapping相关设置则按设置处理，如忽略或抛出异常
   5. **获取sequence Id和Version** 从SequcenceNumberService获取一个sequenceID和Version。SequcenID用于初始化LocalCheckPoint， verion是根据当前Versoin+1用于防止并发写导致数据不一致。
   6. **写入lucene** 这一步开始会对文档uid加锁，然后判断uid对应的version v2和之前update转换时的versoin v1是否一致，不一致则返回第二步重新执行。 如果version一致，如果同id的doc已经存在，则调用lucene的updateDocument接口，如果是新文档则调用lucene的addDoucument. 这里有个问题，如何保证Delete-Then-Add的原子性，ES是通过在Delete之前会加上已refresh锁，禁止被refresh，只有等待Add完成后释放了Refresh Lock, 这样就保证了这个操作的原子性。
   7. **写入translog** 写入Lucene的Segment后，会以key value的形式写Translog， Key是Id, Value是Doc的内容。当查询的时候，如果请求的是GetDocById则可以直接根据_id从translog中获取。满足nosql场景的实时性。
   8. **重构bulk request** 因为primary shard已经将update操作转换为index操作或delete操作，因此要对之前的bulkrequest进行调整，只包含index或delete操作，不需要再进行update的处理操作。
   9. **flush translog** 默认情况下，translog要在此处落盘完成，如果对可靠性要求不高，可以设置translog异步，那么translog的fsync将会异步执行，但是落盘前的数据有丢失风险。
   10. **发送请求给replicas** 将构造好的bulkrequest并发发送给各replicas，等待replica返回，这里需要等待所有的replicas返回，响应请求给协调节点。如果某个shard执行失败，则primary会给master发请求remove该shard。这里会同时把sequenceID， primaryTerm, GlobalCheckPoint等传递给replica。
   11. **等待replica响应** 当所有的replica返回请求时，更细primary shard的LocalCheckPoint。

   参考：

   - [深入理解Elasticsearch写入过程](https://zhuanlan.zhihu.com/p/94915597)
   - [动态更新索引](https://www.elastic.co/guide/cn/elasticsearch/guide/current/dynamic-indices.html)

9. elasticsearch了解多少，说说你们公司 es 的集群架构，索引数据大小，分片有多少，以及一些调优手段 。

   答：我们es采用双机房单集群部署，每个集群三台物理机，后期打算迁往k8s

   目前es部署情况：3个master节点，6个data节点，30+索引，每个索引6分片1副本，目前最大索引是酒店的有400G，600w条数据

   调优手段：

   - 设计阶段调优

     （1）对于需要分词的字段，设置合理的分词器；

     （2）使用别名进行索引管理；

     （3）禁止os将es进程swap出去；

     ​		 swap原理是将磁盘当做虚拟内存来使用，会极大降低es查询效率；

     （4）使用自动生成的id（auto-generated ids）；

     ​         索引具有显式id的文档时，Elasticsearch需要检查具有相同id的文档是否已经存在于相同的分片中，这是昂贵的操作，并随着索引增长而变得更加昂贵。 通过使用自动生成的ID，Elasticsearch可以跳过这个检查，这使索引更快

   - 写入调优

     （1）写入前副本数设置为0；

     （2）写入前关闭 refresh_interval 设置为-1，禁用刷新机制；

     （3）filesystem cache

   - 查询优化

     （1）禁用wildcard、prefix等查询

   还有一些调优方式，请参考：[ES官方调优指南翻译](http://wangnan.tech/post/elasticsearch-how-to/)

10. es有几种node？每个node职责和作用是怎样的？

   答：es主要有4种节点类型，分别是master、data、coordinating（协作节点）、ingest，对应职责分别如下：

   - master：主要负责集群中索引的创建、删除以及数据的Rebalance等操作。
   - data：主要负责集群中数据的索引和检索。
   - coordinating：协调各数据节点，回应客户端请求，比如搜索请求。
   - ingest：专门对索引的文档做预处理，实际中不常用，除非文档在索引之前有大量的预处理工作需要做。

   详细参考

   - https://www.elastic.co/guide/en/elasticsearch/reference/master/ingest.html#ingest

   - [Elasticsearch（ES）集群中节点的角色](https://www.jianshu.com/p/7c4818dda91a)
   - [[Elasticsearch配置项(二)]Node,Threadpool模块配置](https://yemengying.com/2016/03/21/elasticsearch-settings2/)

   

11. elasticsearch的倒排索引是什么？

   答：倒排索引，是通过分词策略，形成了词和文章的映射关系表，这种词典+映射表即为倒排索引。有了倒排索引，就能实现 o（1）时间复杂度的效率检索文章了，极大的提高了检索效率。

   ![](http://tc.ganzhiqiang.wang/1598759075.png?imageMogr2/thumbnail/!70p)

   加分项：倒排索引的底层实现是基于：FST（Finite State Transducer）数据结构，类似Trie树的数据结构。

   lucene 从 4+版本后开始大量使用的数据结构是 FST。FST 有两个优点：

   （1）空间占用小。通过对词典中单词前缀和后缀的重复利用，压缩了存储空间；

   （2）查询速度快。O(len(str))的查询时间复杂度。

11. Elasticsearch 是如何实现 Master 选举的？

   答：那我说一下初始启动场景下，es的master选举过程，假设有三个节点node1，node2，node3。node1启动的时候，执行findMaster()，node1发现只有自己一个node，不满足节点数大于n/2+1的条件（n是参数minimum_master_nodes配置），没办法选举master，然后node1会不断的执行while循环直到找到master。接着node2上线，node1和node2构成了两个节点，当node2选举自己作为master节点时, 并且node2通过ping可以发现node1, 所以此时有两个master候选节点，满足配置条件，故node2就成为master。

   参考：[Elasticsearch的选举机制](https://www.jianshu.com/p/bba684897544)

11. 详细描述一下es的搜索流程？

    答：es搜索流程主要为“query-then-fetch”

    - 客户端发送请求到一个协调节点（coordinate node）
    - 协调节点将搜索请求转发到所有的shard对应的主分片（primary shard）或副分片（replica shard）
    - query phase 每个shard将自己的搜索结果（本质上就是一些doc id），返回给 协调节点（coordinate node），由协调节点（coordinate node）进行数据的合并、排序、分页等，以生成最终结果
    - fetch phase 接着由协调节点（coordinate node），根据doc id去各节点中拉取实际的 `document`数据,最终返回给客户端

12. 详细描述一下es的索引过程？

    - 客户写集群某节点写入数据，发送请求。（如果没有指定路由/协调节点，请求的节点扮演路由节点的角色。）

    - 节点 1 接受到请求后，使用文档_id 来确定文档属于分片 0。请求会被转到另外的节点，假定节点 3。因此分片 0 的主分片分配到节点 3 上。

    - 节点 3 在主分片上执行写操作，如果成功，则将请求并行转发到节点 1和节点 2 的副本分片上，等待结果返回。所有的副本分片都报告成功，节点 3 将向协调节点（节点 1）报告成功，节点 1 向请求客户端报告写入成功。

    如果面试官再问：第二步中的文档获取分片的过程？

    回答：借助路由算法获取，路由算法就是根据路由和文档 id 计算目标的分片 id 的过程。

    ```java
    1shard = hash(_routing) % (num_of_primary_shards)
    ```

13. 能在再详细索引时分片内部的过程吗？

    - 当分片所在的节点接收到来自协调节点的请求后，会将请求写入到 MemoryBuffer，然后定时（默认是每隔 1 秒）写入到 Filesystem Cache，这个从 MomeryBuffer 到 Filesystem Cache 的过程就叫做 refresh；

    - 当然在某些情况下，存在 Momery Buffer 和 Filesystem Cache 的数据可能会丢失，ES 是通过 translog 的机制来保证数据的可靠性的。其实现机制是接收到请求后，同时也会写入到 translog 中 ，当 Filesystem cache 中的数据写入到磁盘中时，才会清除掉，这个过程叫做 flush；

    - 在 flush 过程中，内存中的缓冲将被清除，内容被写入一个新段（segment，存储在磁盘中），段的 fsync将创建一个新的提交点，并将内容刷新到磁盘，旧的 translog 将被删除并开始一个新的 translog。

    - flush 触发的时机是定时触发（默认 30 分钟）或者 translog 变得太大（默认为 512M）时；

    大致流程

    <img src="http://tc.ganzhiqiang.wang/es-shard1.png?imageMogr2/thumbnail/!70p" style="zoom:18%;" />

14. BM25分是如何计算的

    参考：[笔记十九：搜索的相关性算分](https://learnku.com/articles/36132)

### es查询语句相关

1. es常用的查询语句有哪些

   答：[https://chenjiabing666.github.io/2018/09/02/es%E5%90%84%E7%A7%8D%E6%9F%A5%E8%AF%A2/](https://chenjiabing666.github.io/2018/09/02/es各种查询/)

2. 你们前缀查询为什么用edge_ngram，不用prefix查询？

   答：主要是因为prefix查询的性能比较差，需要遍历索引。它类似一个过滤器，不会计算相关性得分，当数据量较小时可以使用。
   
3. Multi Match多字段查询?

   查询由以下type：

   - best_fields  　（默认）查找与任何字段匹配的文档，但使用最佳字段中的_score。看[best_fields](https://www.elastic.co/guide/en/elasticsearch/reference/5.0/query-dsl-multi-match-query.html#type-best-fields)._
   - most_fields　　查找与任何字段匹配的文档，并联合每个字段的_score.
   - cross_fields　　采用相同分析器处理字段，就好像他们是一个大的字段。在每个字段中查找每个单词。看[cross_fields](https://www.elastic.co/guide/en/elasticsearch/reference/5.0/query-dsl-multi-match-query.html#type-cross-fields)。

   参考：[Multi Match Query](Multi Match Query)

## 算法面试题

1. Double Array Trie树的公式是什么？

   答：base[s] + c = t 且 check[t] = s，其中s为父节点位置，t为子节点位置

## 参考文档

- [2019年常见ElasticSearch 面试题解析（上）](https://juejin.im/post/6844904031555420167)
- [2019年常见Elasticsearch 面试题答案详细解析（下）](https://juejin.im/post/6844904032083902471)