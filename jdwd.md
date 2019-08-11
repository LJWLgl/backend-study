# Vesta(C中间层)
### 本人负责模块
- 收藏（梁海军）
- 下单、订单通知、短信通知（段保涛）
- 日志切面、域名切换、HttpClient优化等基础维护（余其顺）
- 太阳码、砍价风控（魏齐虎）
### 资料
- [C中间层开发注意事项](http://conf.ctripcorp.com/pages/viewpage.action?pageId=176087598)
- [T中间层日志](http://conf.ctripcorp.com/pages/viewpage.action?pageId=183499160)
- [域名配置](http://conf.ctripcorp.com/pages/viewpage.action?pageId=183494238)
# 价格服务
本人主要负责了价格下载接口和可定检查接口
**价格下载（getBatchSpacePrice）**
该接口会返回入离日期内房源的最低价，价格会以缓存的价格为基础，当满足使用优惠券和活动的条件时，会减去优惠券和活动优惠的金额。该接口较为复杂，不建议再维护。
**可定检查（checkAvailability）**
该接口本来设计目的会返回房源可不可订，但是现在返回了很多信息，比如房屋最新的价格、清洁费和加人费等，比较臃肿，后面如果要重新使用，建议重做。
# 风控
风控一期，我负责创建风控项目，目前已经接入Apollo、Tshedule、Mysql、Redis等框架，下一步直接调用`kie-server`提供API即可
### 项目地址
[http://gitlab.corp.tujia.com/bi/bnb-thunder](http://gitlab.corp.tujia.com/bi/bnb-thunder)
### 项目发布
项目部署在T2环境，发布可以找侍宇雨支持
### 查看日志
```bash
# 登录跳板机
ssh -i ~/config/tujia/id_rsa zhiqiangg@172.31.90.46
# 登录docker
heli bingo thunder zhanghu.config
# 查询日志
cat /home/tujia/www/bnb-thunder-provider/logs/catalina.out  | grep 'xxx'
```
### DB
T2环境已经申请了一个DB（`tns_thunder_t2`）
### 资料
- [途家新项目创建](http://wiki.corp.tujia.com/confluence/pages/viewpage.action?pageId=23933857)
- [途家Mysql开发设计规范](http://wiki.corp.tujia.com/confluence/pages/viewpage.action?pageId=5321137)
- [Mysql上线流程](http://wiki.corp.tujia.com/confluence/pages/viewpage.action?pageId=5312628)
# bnb-flink-user
### 项目介绍
该项目是民宿宫格实时收集并分析用户一定时间内的行为数据，针对不同用户进行房屋排序的项目即个性化推荐项目，收集维度有用户收藏、用户点击、用户下单，收集的内容主要是用户ID和房源信息，流程大致如下：首先使用Flink实时监听用户行为的ubt消息，然后将数据清洗之后存入Redis， 与此同时将过期的数据删除。另外，BI也会从`Hive`中跑一份`T+1`的离线ubt数据存入`Redis`中，当用户再次进入列表页时，查询服务会依据`Redis`中的行为数据，通过 xgboost 训练数据，用户下次触发后给出推荐的房屋排序。
### 本地调试
 FlinkUser的`isLocal`变量改为true，启动调试FlinkUser的`Main`方法即可
### 项目发布
1. FlinkUser的`isLocal`变量改为false
2. 修改pom version
3. 使用`mvn clean package -Pprod`打包项目
4. 在[Muise携程实时数据平台](http://realtime.fx.ctripcorp.com/#/flink)，找到`flink_bnb_info_analysis`Job，然后上传Jar包并启动
### 日志查询
直接在`Clog`平台查询即可，AppId是`100017406`
### 资料
- [民宿宫格埋点](http://conf.ctripcorp.com/pages/viewpage.action?pageId=167348151)
- [Flink Portal使用说明](http://conf.ctripcorp.com/pages/viewpage.action?pageId=160619154)
- [UBT用户手册](http://docs.ubt.ctripcorp.com/books/ubt-manual)
- [酒店埋点](http://conf.ctripcorp.com/pages/viewpage.action?pageId=165718547)
- [酒店埋点文档汇总](http://conf.ctripcorp.com/pages/viewpage.action?pageId=61546313)
- [Muise用户使用指南](http://conf.ctripcorp.com/pages/viewpage.action?pageId=61565705)
- [离线数据datax脚本](http://zeus.bi.ctripcorp.com/zeus-web/#!/dispatch/job/251000)
# bnb-db-change-listenner
请参考：[db-change-listener使用教程](http://conf.ctripcorp.com/pages/viewpage.action?pageId=168842598)