# 目录
- [Lucene](#lucene)
   - [源码](#源码)
      - [编译lucene源码](#编译lucene源码)
   - [原理](#原理)
      - [lucene底层结构](#lucene底层结构)
      - [lucene优化](#lucene优化)
      - [lucene分词](#lucene分词)
- [ElasticSearch](#elasticsearch)
   - [ES相关原理](#es相关原理)
      - [编译ES源码](#编译es源码)
   - [ES运维](#es运维)
      - [安装ES](#安装es)
      - [集群管理](#集群管理)
      - [调优](#调优)
   - [客户端](#客户端)
      - [High Level Client](#high-level-client)
   - [ES查询](#es查询)
      - [聚合查询](#聚合查询)
      - [ES分词器](#es分词器)
      - [ES查询语句](#es查询语句)
      - [ES计算文本相似度](#es计算文本相似度)
      - [ES算分原理](#es算分原理)
   - [ES插件二次开发](#es插件二次开发)
      - [问题](#问题)

# Lucene

## 源码
### 编译lucene源码
- [Intellij idea搭建solr源码debug调试环境](http://qianjiasong.com/post/solr-debug-idea-build/):star:
## 原理

### lucene底层结构
- [Day 7 - Elasticsearch中数据是如何存储的](https://elasticsearch.cn/article/6178)
- [lucene字典实现原理——FST](https://www.cnblogs.com/bonelee/p/6226185.html):star:
- [[Lucene底层实现原理，它的索引结构](https://www.cnblogs.com/sessionbest/articles/8689030.html)]:star:

### lucene优化
- [Lucene底层原理和优化经验分享(2)-Lucene优化经验总结](https://blog.csdn.net/njpjsoftdev/article/details/54133548)
### lucene分词
- [IK分词器 原理分析 源码解析](https://www.cnblogs.com/jpfss/p/11413473.html)
- [Apache Lucene(全文检索引擎)—分词器](https://www.cnblogs.com/hanyinglong/p/5395600.html#_label3)
- [全文检索lucene中文分词的一些总结](https://my.oschina.net/sunzy/blog/152316)

# ElasticSearch
## ES相关原理
### 编译ES源码
- [ElasticSearch源码解读一：源码编译和Debug环境搭建](https://lanffy.github.io/2019/04/08/Elasticsearch-Compile-Source-And-Debug)
- [Elasticsearch源码解读六：ES中的倒排索引](https://lanffy.github.io/2019/05/10/Inverted-Index-In-Elasticsearch)

## ES运维
### 安装ES
- [docker安装ES & Kibana](https://juejin.im/entry/6844903558425346055)
不建议采用docker安装，因为装插件比较麻烦
### 集群管理
- [elasticsearch系列八：ES 集群管理（集群规划、集群搭建、集群管理）](https://www.cnblogs.com/leesmall/p/9220535.html)
### 调优
- [ES官方调优指南翻译](http://wangnan.tech/post/elasticsearch-how-to/)

## 客户端
### High Level Client
- [Elasitcsearch High Level Rest Client学习笔记（一）](https://my.oschina.net/muziH/blog/1845396)
- [Elasitcsearch High Level Rest Client学习笔记（二） 基础API ](https://my.oschina.net/muziH/blog/1858134)
- [Elasticsearch的路由（Routing）特性](https://my.oschina.net/muziH/blog/1845783)
- [使用Java High Level REST Client操作elasticsearch](https://www.cnblogs.com/ginb/p/8716485.html)
## ES索引
- [深入理解Elasticsearch写入过程](https://zhuanlan.zhihu.com/p/94915597)
## ES查询
### 聚合查询
- [Elasticsearch 聚合分析深入学习](https://zhuanlan.zhihu.com/p/107820698):star::star:
- [ES系列八、正排索Doc Values和Field Data](https://www.cnblogs.com/wangzhuxing/p/9508784.html):star:
### ES分词器
- [Tokenizer reference](https://www.elastic.co/guide/en/elasticsearch/reference/current/analysis-tokenizers.html)
- [ES分词器（翻译）](https://blog.csdn.net/jacksonary/article/details/83902325)

### ES查询语句
- [es各种查询](https://chenjiabing666.github.io/2018/09/02/es%E5%90%84%E7%A7%8D%E6%9F%A5%E8%AF%A2/)
### ES计算文本相似度
### ES算分原理
- [ElasticSearch评分分析 explian 解释和一些查询理解](https://www.cnblogs.com/hapjin/p/9677753.html):star::star:
- [向量空间模型(Vector Space Model)的理解（解释了TF-IDF算分逻辑）](https://www.cnblogs.com/hapjin/p/8687527.html)
- [Elasticsearch源码解读五：搜索相关性排序算法详解](https://lanffy.github.io/2019/05/08/Elasticsearch-Search-Score-Algorithm)
- [搜索引擎中相似度算法TF-IDF和BM25](http://qianjiasong.com/post/nlp-tf-idf-bm25/)

## ES插件二次开发
### 问题
1. 解决Java安全策略（java.policy）
   - [java安全管理器SecurityManager入门](https://www.cnblogs.com/duanxz/p/6108357.html)
   - [如何禁用Java安全管理器](https://cloud.tencent.com/developer/ask/69667)
   - [ java安全沙箱（四）之安全管理器及Java API ](https://www.cnblogs.com/duanxz/p/6108357.html)



