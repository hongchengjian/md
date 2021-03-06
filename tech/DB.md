

Table of Contents
=================

* [NoSQL VS RDMS](#nosql-vs-rdms)
  * [RDMS ACID常见问题](#rdms-acid%E5%B8%B8%E8%A7%81%E9%97%AE%E9%A2%98)
  * [RDMS ACID路线和总结](#rdms-acid%E8%B7%AF%E7%BA%BF%E5%92%8C%E6%80%BB%E7%BB%93)
  * [高可用：并行处理和分布式系统的日志复制和重演](#%E9%AB%98%E5%8F%AF%E7%94%A8%E5%B9%B6%E8%A1%8C%E5%A4%84%E7%90%86%E5%92%8C%E5%88%86%E5%B8%83%E5%BC%8F%E7%B3%BB%E7%BB%9F%E7%9A%84%E6%97%A5%E5%BF%97%E5%A4%8D%E5%88%B6%E5%92%8C%E9%87%8D%E6%BC%94)
* [NoSQL](#nosql)
  * [NoSQL解决了什么问题](#nosql%E8%A7%A3%E5%86%B3%E4%BA%86%E4%BB%80%E4%B9%88%E9%97%AE%E9%A2%98)
* [选型](#%E9%80%89%E5%9E%8B)
  * [说明](#%E8%AF%B4%E6%98%8E)
  * [Storm VS Flink VS Spark Streaming](#storm-vs-flink-vs-spark-streaming)
    * [Flink优势](#flink%E4%BC%98%E5%8A%BF)
  * [流计算 VS 批处理](#%E6%B5%81%E8%AE%A1%E7%AE%97-vs-%E6%89%B9%E5%A4%84%E7%90%86)
  * [实时计算](#%E5%AE%9E%E6%97%B6%E8%AE%A1%E7%AE%97)
  * [实时计算 VS 搜索](#%E5%AE%9E%E6%97%B6%E8%AE%A1%E7%AE%97-vs-%E6%90%9C%E7%B4%A2)
* [Flink](#flink)
  * [Flink落地](#flink%E8%90%BD%E5%9C%B0)
    * [淘宝](#%E6%B7%98%E5%AE%9D)
    * [有赞](#%E6%9C%89%E8%B5%9E)
    * [汇智](#%E6%B1%87%E6%99%BA)
      * [商品统计](#%E5%95%86%E5%93%81%E7%BB%9F%E8%AE%A1)
      * [实时在线统计](#%E5%AE%9E%E6%97%B6%E5%9C%A8%E7%BA%BF%E7%BB%9F%E8%AE%A1)
  * [Flink展望](#flink%E5%B1%95%E6%9C%9B)
  * [Flink在Yarn上部署](#flink%E5%9C%A8yarn%E4%B8%8A%E9%83%A8%E7%BD%B2)
  * [Flink CEP](#flink-cep)
  * [Flink使用问题](#flink%E4%BD%BF%E7%94%A8%E9%97%AE%E9%A2%98)
    * [(1)Single Job模式下实际收到的 Container数量超过了配置的数量，并且没有被回收](#1single-job%E6%A8%A1%E5%BC%8F%E4%B8%8B%E5%AE%9E%E9%99%85%E6%94%B6%E5%88%B0%E7%9A%84-container%E6%95%B0%E9%87%8F%E8%B6%85%E8%BF%87%E4%BA%86%E9%85%8D%E7%BD%AE%E7%9A%84%E6%95%B0%E9%87%8F%E5%B9%B6%E4%B8%94%E6%B2%A1%E6%9C%89%E8%A2%AB%E5%9B%9E%E6%94%B6)
    * [(2)延时监控](#2%E5%BB%B6%E6%97%B6%E7%9B%91%E6%8E%A7)
    * [(3)用户代码中启用SpringContext，在Task执行过程中去获取Bean](#3%E7%94%A8%E6%88%B7%E4%BB%A3%E7%A0%81%E4%B8%AD%E5%90%AF%E7%94%A8springcontext%E5%9C%A8task%E6%89%A7%E8%A1%8C%E8%BF%87%E7%A8%8B%E4%B8%AD%E5%8E%BB%E8%8E%B7%E5%8F%96bean)
    * [(4)在实际执行function的open方法中通过配置文件获取SpringContext](#4%E5%9C%A8%E5%AE%9E%E9%99%85%E6%89%A7%E8%A1%8Cfunction%E7%9A%84open%E6%96%B9%E6%B3%95%E4%B8%AD%E9%80%9A%E8%BF%87%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6%E8%8E%B7%E5%8F%96springcontext)
    * [(5)用Dubbo服务的吞吐](#5%E7%94%A8dubbo%E6%9C%8D%E5%8A%A1%E7%9A%84%E5%90%9E%E5%90%90)
* [Spark](#spark)
  * [Spark 3\.0支持7种join](#spark-30%E6%94%AF%E6%8C%817%E7%A7%8Djoin)
* [MySQL Oracle(去IOE)](#mysql-oracle%E5%8E%BBioe)
  * [连接池](#%E8%BF%9E%E6%8E%A5%E6%B1%A0)
  * [数据库排序算法](#%E6%95%B0%E6%8D%AE%E5%BA%93%E6%8E%92%E5%BA%8F%E7%AE%97%E6%B3%95)
  * [MySQL&gt;=5\.7(2020\-10\-21 已发布8\.0版本) Oracle  &gt;= 11g数据库规范](#mysql572020-10-21-%E5%B7%B2%E5%8F%91%E5%B8%8380%E7%89%88%E6%9C%AC-oracle---11g%E6%95%B0%E6%8D%AE%E5%BA%93%E8%A7%84%E8%8C%83)
  * [设计](#%E8%AE%BE%E8%AE%A1)
    * [SQL自动检查](#sql%E8%87%AA%E5%8A%A8%E6%A3%80%E6%9F%A5)
    * [SQL优化点](#sql%E4%BC%98%E5%8C%96%E7%82%B9)
  * [MySQL crash recovery](#mysql-crash-recovery)
  * [binlog](#binlog)
    * [开启binlog](#%E5%BC%80%E5%90%AFbinlog)
    * [Kafka binlog全局有序](#kafka-binlog%E5%85%A8%E5%B1%80%E6%9C%89%E5%BA%8F)
    * [binlog缓存问题](#binlog%E7%BC%93%E5%AD%98%E9%97%AE%E9%A2%98)
    * [show binlog events;](#show-binlog-events)
    * [利用bin\_log恢复数据](#%E5%88%A9%E7%94%A8bin_log%E6%81%A2%E5%A4%8D%E6%95%B0%E6%8D%AE)
    * [Canal](#canal)
  * [show variables](#show-variables)
      * [autocommit](#autocommit)
    * [SQL\_SAFE\_UPDATES](#sql_safe_updates)
  * [死锁问题](#%E6%AD%BB%E9%94%81%E9%97%AE%E9%A2%98)
  * [存储引擎](#%E5%AD%98%E5%82%A8%E5%BC%95%E6%93%8E)
    * [MySQL5\.7支持的存储引擎](#mysql57%E6%94%AF%E6%8C%81%E7%9A%84%E5%AD%98%E5%82%A8%E5%BC%95%E6%93%8E)
  * [事务](#%E4%BA%8B%E5%8A%A1)
    * [原理](#%E5%8E%9F%E7%90%86)
    * [事务管理器TransactionManager](#%E4%BA%8B%E5%8A%A1%E7%AE%A1%E7%90%86%E5%99%A8transactionmanager)
    * [MySQL事务隔离级别](#mysql%E4%BA%8B%E5%8A%A1%E9%9A%94%E7%A6%BB%E7%BA%A7%E5%88%AB)
      * [脏、幻读（虚读）](#%E8%84%8F%E5%B9%BB%E8%AF%BB%E8%99%9A%E8%AF%BB)
    * [事务传播机制](#%E4%BA%8B%E5%8A%A1%E4%BC%A0%E6%92%AD%E6%9C%BA%E5%88%B6)
    * [事务回滚](#%E4%BA%8B%E5%8A%A1%E5%9B%9E%E6%BB%9A)
  * [锁](#%E9%94%81)
    * [GEN\_CLUST\_INDEX死锁](#gen_clust_index%E6%AD%BB%E9%94%81)
  * [索引](#%E7%B4%A2%E5%BC%95)
    * [MySQL索引类型](#mysql%E7%B4%A2%E5%BC%95%E7%B1%BB%E5%9E%8B)
    * [MySQL索引失效](#mysql%E7%B4%A2%E5%BC%95%E5%A4%B1%E6%95%88)
    * [MySQL复合索引ABC问题](#mysql%E5%A4%8D%E5%90%88%E7%B4%A2%E5%BC%95abc%E9%97%AE%E9%A2%98)
    * [MySQL复合索引最左原则底层原理](#mysql%E5%A4%8D%E5%90%88%E7%B4%A2%E5%BC%95%E6%9C%80%E5%B7%A6%E5%8E%9F%E5%88%99%E5%BA%95%E5%B1%82%E5%8E%9F%E7%90%86)
  * [MySQL explain](#mysql-explain)
    * [Hive SQL VS SQL](#hive-sql-vs-sql)
    * [分号符处理](#%E5%88%86%E5%8F%B7%E7%AC%A6%E5%A4%84%E7%90%86)
  * [MySQL join](#mysql-join)
* [Hive](#hive)
  * [Hive中文件存储格式及文件压缩方式](#hive%E4%B8%AD%E6%96%87%E4%BB%B6%E5%AD%98%E5%82%A8%E6%A0%BC%E5%BC%8F%E5%8F%8A%E6%96%87%E4%BB%B6%E5%8E%8B%E7%BC%A9%E6%96%B9%E5%BC%8F)
  * [Hive中三种自定义函数](#hive%E4%B8%AD%E4%B8%89%E7%A7%8D%E8%87%AA%E5%AE%9A%E4%B9%89%E5%87%BD%E6%95%B0)
  * [Hive的数据类型](#hive%E7%9A%84%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
    * [简单数据类型](#%E7%AE%80%E5%8D%95%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
    * [复杂数据类型](#%E5%A4%8D%E6%9D%82%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
    * [NULL类型](#null%E7%B1%BB%E5%9E%8B)
  * [Hive四种表类型](#hive%E5%9B%9B%E7%A7%8D%E8%A1%A8%E7%B1%BB%E5%9E%8B)
  * [Hive元数据三种保存方式](#hive%E5%85%83%E6%95%B0%E6%8D%AE%E4%B8%89%E7%A7%8D%E4%BF%9D%E5%AD%98%E6%96%B9%E5%BC%8F)
  * [Hive数仓分层](#hive%E6%95%B0%E4%BB%93%E5%88%86%E5%B1%82)
  * [HiveSQL转化成MR过程](#hivesql%E8%BD%AC%E5%8C%96%E6%88%90mr%E8%BF%87%E7%A8%8B)
  * [Hive与数据库交互](#hive%E4%B8%8E%E6%95%B0%E6%8D%AE%E5%BA%93%E4%BA%A4%E4%BA%92)
  * [Hive数据倾斜](#hive%E6%95%B0%E6%8D%AE%E5%80%BE%E6%96%9C)
    * [原因](#%E5%8E%9F%E5%9B%A0)
    * [解决方案](#%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88)
    * [Ex\.SQL调节](#exsql%E8%B0%83%E8%8A%82)
  * [Sort By VS Order By VS Cluster By VS Distribute By](#sort-by-vs-order-by-vs-cluster-by-vs-distribute-by)
  * [Hive优化](#hive%E4%BC%98%E5%8C%96)
  * [HiveQL](#hiveql)
* [HBase](#hbase)
  * [中间件持久化功能](#%E4%B8%AD%E9%97%B4%E4%BB%B6%E6%8C%81%E4%B9%85%E5%8C%96%E5%8A%9F%E8%83%BD)
  * [HBase Salting](#hbase-salting)
* [Redis](#redis)
  * [Redis VS Tair VS MemCache](#redis-vs-tair-vs-memcache)
  * [Epoll指令](#epoll%E6%8C%87%E4%BB%A4)
  * [FD](#fd)
  * [Epoll VS Select/Poll](#epoll-vs-selectpoll)
  * [集群模式](#%E9%9B%86%E7%BE%A4%E6%A8%A1%E5%BC%8F)
    * [(1)主从](#1%E4%B8%BB%E4%BB%8E)
      * [主从复制细节原理](#%E4%B8%BB%E4%BB%8E%E5%A4%8D%E5%88%B6%E7%BB%86%E8%8A%82%E5%8E%9F%E7%90%86)
        * [全量同步](#%E5%85%A8%E9%87%8F%E5%90%8C%E6%AD%A5)
        * [增量同步](#%E5%A2%9E%E9%87%8F%E5%90%8C%E6%AD%A5)
        * [主从同步策略](#%E4%B8%BB%E4%BB%8E%E5%90%8C%E6%AD%A5%E7%AD%96%E7%95%A5)
        * [主从同步注意点](#%E4%B8%BB%E4%BB%8E%E5%90%8C%E6%AD%A5%E6%B3%A8%E6%84%8F%E7%82%B9)
    * [(2)哨兵](#2%E5%93%A8%E5%85%B5)
    * [(3)代理](#3%E4%BB%A3%E7%90%86)
    * [(4)Redis Cluster 去中心化分片集群](#4redis-cluster-%E5%8E%BB%E4%B8%AD%E5%BF%83%E5%8C%96%E5%88%86%E7%89%87%E9%9B%86%E7%BE%A4)
      * [Redis Cluster VS 传统Redis集群](#redis-cluster-vs-%E4%BC%A0%E7%BB%9Fredis%E9%9B%86%E7%BE%A4)
      * [搭建](#%E6%90%AD%E5%BB%BA)
  * [持久化AOF和RDB](#%E6%8C%81%E4%B9%85%E5%8C%96aof%E5%92%8Crdb)
  * [常用Jar](#%E5%B8%B8%E7%94%A8jar)
  * [数据结构和命令](#%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E5%92%8C%E5%91%BD%E4%BB%A4)
    * [String](#string)
      * [Jedis PIPELINE(微盟面试题)](#jedis-pipeline%E5%BE%AE%E7%9B%9F%E9%9D%A2%E8%AF%95%E9%A2%98)
    * [Hash](#hash)
    * [List](#list)
    * [Set](#set)
    * [ZSet](#zset)
    * [其他](#%E5%85%B6%E4%BB%96)
  * [Redis扩容和缩容](#redis%E6%89%A9%E5%AE%B9%E5%92%8C%E7%BC%A9%E5%AE%B9)
  * [缓存一致性](#%E7%BC%93%E5%AD%98%E4%B8%80%E8%87%B4%E6%80%A7)
    * [Scenario](#scenario)
    * [A\.外部依赖](#a%E5%A4%96%E9%83%A8%E4%BE%9D%E8%B5%96)
    * [B\.缓存和DB一致性](#b%E7%BC%93%E5%AD%98%E5%92%8Cdb%E4%B8%80%E8%87%B4%E6%80%A7)
      * [问题(1)先写缓存，后写DB](#%E9%97%AE%E9%A2%981%E5%85%88%E5%86%99%E7%BC%93%E5%AD%98%E5%90%8E%E5%86%99db)
      * [问题(2)若先写DB，后写缓存](#%E9%97%AE%E9%A2%982%E8%8B%A5%E5%85%88%E5%86%99db%E5%90%8E%E5%86%99%E7%BC%93%E5%AD%98)
      * [解决方案\-读写分离\+状态机（注意顺序）](#%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88-%E8%AF%BB%E5%86%99%E5%88%86%E7%A6%BB%E7%8A%B6%E6%80%81%E6%9C%BA%E6%B3%A8%E6%84%8F%E9%A1%BA%E5%BA%8F)
      * [补充：数据库发生变化，如何及时更新缓存](#%E8%A1%A5%E5%85%85%E6%95%B0%E6%8D%AE%E5%BA%93%E5%8F%91%E7%94%9F%E5%8F%98%E5%8C%96%E5%A6%82%E4%BD%95%E5%8F%8A%E6%97%B6%E6%9B%B4%E6%96%B0%E7%BC%93%E5%AD%98)
  * [缓存失效策略](#%E7%BC%93%E5%AD%98%E5%A4%B1%E6%95%88%E7%AD%96%E7%95%A5)
    * [定时删除（内存友好）](#%E5%AE%9A%E6%97%B6%E5%88%A0%E9%99%A4%E5%86%85%E5%AD%98%E5%8F%8B%E5%A5%BD)
    * [惰性删除（CPU友好）](#%E6%83%B0%E6%80%A7%E5%88%A0%E9%99%A4cpu%E5%8F%8B%E5%A5%BD)
    * [缓存命中率](#%E7%BC%93%E5%AD%98%E5%91%BD%E4%B8%AD%E7%8E%87)
  * [缓存雪崩、降级、穿透、预热](#%E7%BC%93%E5%AD%98%E9%9B%AA%E5%B4%A9%E9%99%8D%E7%BA%A7%E7%A9%BF%E9%80%8F%E9%A2%84%E7%83%AD)
    * [缓存雪崩](#%E7%BC%93%E5%AD%98%E9%9B%AA%E5%B4%A9)
    * [缓存降级](#%E7%BC%93%E5%AD%98%E9%99%8D%E7%BA%A7)
    * [缓存穿透](#%E7%BC%93%E5%AD%98%E7%A9%BF%E9%80%8F)
    * [缓存预热](#%E7%BC%93%E5%AD%98%E9%A2%84%E7%83%AD)
  * [事务](#%E4%BA%8B%E5%8A%A1-1)
    * [选型RDB VS AOF](#%E9%80%89%E5%9E%8Brdb-vs-aof)
  * [问题集](#%E9%97%AE%E9%A2%98%E9%9B%86)
    * [Redis单个Key超过512M？](#redis%E5%8D%95%E4%B8%AAkey%E8%B6%85%E8%BF%87512m)
    * [为什么RedisCluster有16384个槽？](#%E4%B8%BA%E4%BB%80%E4%B9%88rediscluster%E6%9C%8916384%E4%B8%AA%E6%A7%BD)
    * [CRC16 hash VS 一致性Hash](#crc16-hash-vs-%E4%B8%80%E8%87%B4%E6%80%A7hash)
* [HDFS](#hdfs)
* [Flume](#flume)
* [Kylin](#kylin)
* [Storm(快被淘汰)](#storm%E5%BF%AB%E8%A2%AB%E6%B7%98%E6%B1%B0)
* [Yarn](#yarn)
* [Mesos](#mesos)
* [Hibernate](#hibernate)
* [Mybatis VS JPA VS SpringData](#mybatis-vs-jpa-vs-springdata)
* [Mybatis](#mybatis)
  * [Mybatis Plugin(阿里面试题)](#mybatis-plugin%E9%98%BF%E9%87%8C%E9%9D%A2%E8%AF%95%E9%A2%98)
  * [Mybatis数据类型](#mybatis%E6%95%B0%E6%8D%AE%E7%B1%BB%E5%9E%8B)
  * [Mybatis  Plus update null](#mybatis--plus-update-null)
  * [Mybatis Plus 删除和逻辑删除](#mybatis-plus-%E5%88%A0%E9%99%A4%E5%92%8C%E9%80%BB%E8%BE%91%E5%88%A0%E9%99%A4)
  * [Mybatis where 1=1造成sql注入](#mybatis-where-11%E9%80%A0%E6%88%90sql%E6%B3%A8%E5%85%A5)
  * [Mybatis Plus分页](#mybatis-plus%E5%88%86%E9%A1%B5)

Created by [gh-md-toc](https://github.com/ekalinin/github-markdown-toc.go)

作者：cj

# NoSQL VS RDMS

## RDMS ACID常见问题

```css
RDMS ACID————C consistency非常重要 
Q1:ACID中的C VS CAP中的C VS 数据一致性(贝壳面试题)
Q2:什么是数据库一致性C？
Q3:OS层锁与并发控制Atomic VS 数据库层锁与并发控制  粒度、类型、实现方式几个出发点思考
数据库并发控制自由性更高：选择使用lock，也可以选择commit protocol
Q4:分布式任务调度下的数据一致性
commit protocol是允许先做dirty read然后rollback，锁的存在更多是根本不允许事务做dirty read
```

```css
概念角度理解：参考书 Database System Concepts
实践角度理解：Innodb开源代码
```

## RDMS ACID路线和总结

```css
路线：最基础的一致性C -> Redo保证持久性D、Undo保证原子性A -> 并行事务一致性 -> 引入隔离性I -> 实现隔离性I(悲观和乐观锁) -> 死锁 -> 两阶段锁协议、死锁检测解决死锁

隔离性I悲观 为了性能 粒度(数据库级、表级、行级)  性质(共享锁、排他锁、共享意向锁、排他意向锁、共享排他意向锁)
隔离性I乐观 不同事务可同时看到同一对象(数据行)的不同历史版本，若两个事务同时修改了同一数据行，在较晚的事务提交时进行冲突检测 两种实现(1)通过日志Undo获取数据行历史版本 (2)在内存中保存同一数据行的多个历史版本，时间戳来区分
```



```css
一致性C是最基础的，其他三个AID是为了保证一致性而存在的。
数据库实现场景下，一致性C分为数据库外部的一致性(某个应用执行A转账B操作时，必须在同一个事务内部调用对A减和对B增的操作)与数据库内部的一致性(一个事务里的多个操作全部成功或全部失败，部分成功抛错回滚后也是全部失败)

原子性A并不能完全保证一致性C，为了保证事务原子性A，必须通过日志Redo/Undo。所有对数据的更新操作都写入日志，若一个事务中的一部分操作已经成功，但其他的操作由于断电、系统奔溃、软硬件错误无法继续，则通过回溯日志将已经执行成功的操作撤销，达到全部操作失败目的。

数据库系统崩溃后重启，此时数据处于不一致状态，必须先执行crash recovery(ref {待补充详细后url})，读取日志进行Redo(重演将所有已执行成功但尚未写入磁盘的操作，保证持久性D)，再对所有到崩溃时尚未成功提交的事务进行Undo(撤销所有执行一部分呢但尚未提交的操作，保证原子性A)。crash recovery结束后数据库恢复到一致性状态，可以继续被使用。

多个事务并行，即使保证了每一个事务的原子性，仍可能导致数据不一致。
T1转入A 100，(1)先读A账户值(2)后+100
在(1)和(2)之间，T2修改了A，+100
事实是T1最终完成，但A只增加了100，T2的修改被T1覆盖了

为保证并发下的一致性C，引入隔离性I，即多个事务并发执行后的状态与串行执行后的状态是等价的。
实现

A atomicity:事务里的所有操作是一个整体，要么全部成功做完，要么不做；所有操作中只要有一个操作失败，整个事务就失败。
C consistency: A转账给B，A的钱减少，B的钱没有增加，数据处于不一致状态
I Isolation: 多个事务并发执行后的状态与串行执行后的状态是等价的。
D Durability: 执行成功的操作都会写入磁盘

```

## 高可用：并行处理和分布式系统的日志复制和重演

# NoSQL

```css
Not only SQL四类
(1)KV存储：Memcached、Redis、Flare
(2)列存储：Hbase、Cassandra
(3)图形存储
(4)文档存储：MongoDB、CouchDB
```

## NoSQL解决了什么问题

# 选型

| 功能点         | MySQL | Oracle | Cassandra | HBase | MongoDB                 | SQL Server | DynamoDB | Spanner | CockroachDB |      |      |
| -------------- | ----- | ------ | --------- | ----- | ----------------------- | ---------- | -------- | ------- | ----------- | ---- | ---- |
| 支持ACID       |       |        |           |       |                         |            |          |         |             |      |      |
| 许可协议       |       |        |           |       |                         |            |          |         |             |      |      |
| 支持分布式事务 |       |        |           |       |                         |            |          |         |             |      |      |
| 协议           |       |        |           |       | Custom, binary（ BSON） |            |          |         |             |      |      |
| 开发语言       |       |        |           |       | C++                     |            |          |         |             |      |      |

## 说明

```css
WAL Write Ahead Log预写日志，所有修改在提交之前都要先写入log文件中，log文件包括redo和undo，若事务失败，WAL中的记录会被忽略，撤销修改；若事务成功，将在随后的某个时间被写回到数据库文件中，提交修改。

数据库最大挑战是磁盘读写，方案三种：随机读写顺序读写，缓冲单条读写改批量读写，单线程读写改并发读写
```



![DB VS](http://hongchengjian.gitee.io/md/img/db/DB%20VS.png)

上面的图其实并没有啥用？过于笼统待删除

## Storm VS Flink VS Spark Streaming

```css
Flink具有如下优势
(1)性能(延迟、吞吐、State)
Storm吞吐量不大，开发成本高，SQL支持不好，状态管理没优势(状态可以依赖Redis)
Spark Streaming 微批，达不到纯流式样引擎效果
Spark Streaming 中间状态全部在内存，Flink 借助于rocksdb(分布式缓存系统)支持吞吐量更大，保存更多状态

(2)Flink SQL支持(一个query包含多个聚合，Distinct去重，窗口)
Spark Streaming一个Query多个聚合会抛异常(Spark Streaming一个Query只能包含一个聚合)
Spark Streaming窗口操作之后无法管理offset，因offset存储于HasOffsetRanges，只有KafkaRDD extends HasOffsetRanges，对KafkaRDD进行转化之后就无法再获取offset了
Spark Streaming不支持去重
Flink窗口 dataFlow输出覆盖支持场景更多

(3)灵活度(抽象层次转换)
Spark Streaming一套API是table，一套API是Dstream，table和Dstream无法相互转换，而Flink可以相互转换

(4)复杂事件处理
Flink有CEP
```

### Flink优势

```css 
(1)Flink提供了 Exactly-once精准语义
Ex. 一个Flink DAG包括一个或多个算子，每个算子有多个并发度，流式wordcount中有2个重要算子：(1)split算子把每个句子拆解成一个一个单词，单词经过shuffle到达第二个算子，(2)第二个算子对每个单词出现的次数进行计数。整个过程像流式的Map reduce，但与Map reduce不同的是第二个计数算子：为了能够计数需要知道一个值到目前为止已经出现了多少次才能在此基础上+1，在Flink之前业务方需要将状态存在外部存储（在分布式系统里这个外部存储出错是不可避免的，当出错时恢复经常多算或少算，很难做到精准的语义）

(2)Flink最大创新是在流计算中引入状态概念，作为流计算引擎将状态管理起来。 checkpoint机制让一个快速流计算作业拍一张全局的快照，当出现错误时，能将系统会滚到上一次成功的快照，保证所有状态的一致性。

(3)Flink跑在Standalone、YARN、K8S、云环境

(4)Flink Runtime负责运行一个分布式DAG，runtime上有各种API层DataSet做批处理，DataStream做流处理
Runtime层扩展了算子的定义，使得Flink流式的算子能更好地处理输入的流式顺序 Ex. Hashjoin算子

(5)Blink在runtime层实现了一个分布式架构，去掉了Flink在集群上性能的单点，各个作业更好的隔离，Flink作业和资源管理能够动态申请、释放，引入了一种抽象能让Flink实现在不同的资源管理器上。基于Credit的流控和反压，解决了原来的死锁问题。作业容错环境下恢复的优化。

(6)API层DataSet做批处理，DataStream做流处理，两个划分导致与流割裂，引入 Query Processor层定义算子，为上层可以共享。
为了阿里业务定义了流式SQL语义，阿里双11 17亿/s的处理速度，集群有万台。索引的全量作业一般时批处理来创建，问题是在批处理完成全量索引创建后的任何更新，需要到下一天才能生效。为了能够提供索引的实时性，解决方案是引入增量流计算完成索引更新，Lambda架构。难度是两套流程，业务复杂时，两套流程具有挑战性。

(7)QueryExecution 引入了二进制表达式，省去了序列化、反序列化开销。
(8)算子对资源可以动态申请、使用，不用担心OutOfMemory问题
(9)Query optimizer优化器基于成本，去决定join的种类、顺序、聚合策略、丰富规则、统计
(10)Flink随数据的增加，性能是Spark的三倍，Flink不依赖于很大的内存，Spark依赖很大的内存
(11)Flink+Hive自由切换
(12)Flink+Zeppelin Table API和SQL

```

## 流计算 VS 批处理

```css
(1)流计算可以在不完整的数据上计算，不需要等待到数据完全到来才进行计算 Ex.流式wordcount：消息队列不断拿一条一条消息，当消息到来时会一条一条处理，每条消息是一个句子，会实时地打印出每个词到目前为止出现过多少次。 
与批处理不一样的是作业会一直在运行，当新消息值到来时会不断更新计算结果。

(2)批处理数据集是有限的，需要完整的数据，可以灵活地改查询SQL，吞吐量很高。
流计算的数据集是无限的，不需要完整的数据，
流式计算批处理更具有优势：流式的shuffle能更好地使用网络、IO、CPU、带宽
```

## 实时计算

```css
放弃MapReduce(IO瓶颈)
适用场景：数据量很大，无法穷举所有可能条件的查询组合，无法预估，数据源不间断的流式数据，实时响应要求高，统计各种组合的分布
```

## 实时计算 VS 搜索

```
实时计算 VS 搜索
搜索目的是排序，实时计算目的是汇总
搜索返回是list，实时计算返回是精确结果
搜索根据权重取TopN做排序，实时计算是获取所有满足条件数据做计算
```

# Flink

```css
实时计算、流计算在机器学习应用，搜索和推荐利用实时特征优化搜索和推荐的结果，商品快要售卖完时不推荐商品
数据产生 --> 数据收集 ---> 数据处理
Flink创始人意识到：流计算作为所有计算场景的抽象。
```

## Flink落地

### 淘宝

```css
阿里每天万亿数据，每天PB，总量数据有EB  双11交易数据的难度：精准1次实时计算
阿里维护的内部Flink叫做Blink
```

### 有赞

```css
数据源：Kafka、NSQ(go中间件上层封了Java Client)
ZanKV兼容分布式Redis协议 YARN部署Single Job模式(每个任务起一个ApllicationMaster隔离性好)
背景很多服务都只暴露了Dubbo接口，在Flink应用中使用Spring
```

### 汇智

```css
规则引擎：规则匹配和规则处理
数据来源于Kafka/DataHub
业务系统是一个Web页面，用户用来定义规则，有一台接口服务器跟业务系统交互，接受规则存在数据库
动态规则，Job运行过程中增加修改删除规则
```

#### 商品统计

```css
场景1:商品统计
假设Kafka中的product_sell表记录是商品的销售信息，需求是客户在业务系统页面输入需要监控的商品号，一旦有该商品的销售信息，必须实时反馈给业务系统
思路1:
每当从业务系统接收到一个需要监控的商品起一个Job select * from product_sell where product_id = XXX
撤销监控时删除Job 
缺陷：要为每种商品各起一个Job，并且要经常启动和删除Job

思路2:
阿里实时计算Flink中维表join实现
要将监控的商品保存在维表中 select * from product_sell,monitor_products where product_sell.product_id = monitor_products.product_id
缺陷：每来一次数据去查一次维表，速度太慢，若将维表内容到内存，如何同步是问题：(1)同步太频繁，则太浪费资源(2)同步间隔太久，则做不到实时更新

思路3:
用UDF来定制实现:
规则保存在Oracle，Job启动时，在UDF的open方法里，把规则从Oracle加载到内存
同时，起一个ZK 监听器，当接受到服务器传来的增加/修改/删除规则请求时，把新的规则加载到内存，当数据从Kafka过来时，直接将商品编号与内存中的比较，若存在内存中，则返回true
udf伪代码
public class ProductMatch extends ScalaFunction{
  private List<String> productIds;
  public open(){
    zookeeper.monitor((operation,productId) -> {
      if("add".equals(operation)){
        productIds.add(productId);
      }
    }
  }
  
  public boolean eval(String productId){
    return productIds.contains(productId);
  }
}

SQL
select from product_sell where Product_Match(product);
```

#### 实时在线统计

```css
场景2:实时在线统计
有一个App会不定时地向服务器上传位置(上报字段包括uid,lon,lat)，上报的位置存在Kafka lbs表里
需求：根据APP上报的位置，每5分钟统计一次重点关注区域(例如某学校、某商场)有多少用户实时在线。
思考：select count(uid) from lbs where is_in_area(lon,lat);
该语句只是算出进入该区域有多少人次，而不是计算出当前有多少人在线
```



##Flink 探索

```css
（1）机器学习PS(Parameter Server)架构：不再需要专门的参数管理服务器来管理参数，取代的是用Flink的状态管理参数，Flink Delta Iteration增量进行参数的更新，效果是优化后处理规模是其他计算引擎的规模十倍以上。
（2）图计算 用Flink状态管理图，用Delta Iteration做增量图的更改
（3）微服务场景 服务之间的调用 线程同步调度会有等待，同步改成异步会压垮微服务，反压机制，自动扩容、缩容能力
微服务的状态存储在外部数据库中，用Flink 状态管理起外部数据库中的数据，Exactly-once模拟事务的方向
```

## Flink展望

```css
(1)实时SQL 之前基于SDK，未来会基于Flink的SQL Client做二次开发
(2)Flink批处理尝试 将Flink批处理能力服务化，VS Spark SQL优劣
(3)Flink ML尝试 VS Spark MLlib
(4)调度和资源管理 Flink将调度器独立成插拔式的模块 资源管理的动态Auto Scaling
```



## Flink在Yarn上部署

```css
TaskExecutor实际任务的执行者，会启动Slot，每个Slot对应具体的子任务，会将自己的状态汇报给Resource Manager
SlotManager Slot管理者，也负责运行中的任务，会向Flink Resource Manager申请新的容器，发起申请但还未拿到Slot会记录在 pending slot里
Flink ResourceManager会向YARN申请容器 
计数器 积压的容器申请
AMRMClient(申请容器)、CallbackHandler(1.当YARN资源申请好时通知Flink Resource Manager 2.当容器异常退出时，也会通知FLink Resource Manager)
```

## Flink CEP

```css
优势：跨事件的复杂处理 缺陷：无法动态修改规则

```



## Flink使用问题

### (1)Single Job模式下实际收到的 Container数量超过了配置的数量，并且没有被回收

正常流程

```css
任务需求：-yn 3 -ys 2 -p 6
3个Container、每个Container有2个Slot，并行度是6

总共需要6个Slot，当前分配了四个，还需2个新的Slot
SlotManager接到请求后发现并没有新的可用的Slot，会将Slot请求积压在Pending Slot中
Pending Slot变成2，向Flink Resource Manager申请Worker
Flink YARN Resource Manager向YARN申请container，pending container request置1
YARN RM准备好Container，CallbackHandler接受到通知，接收container并更新pending container request置0
在Container中启动TaskExecutor
TaskExecutor向SlotManager 注册2个空的Slot，2个空Slot就可以满足前面积压的2个Slot申请
```

问题流程

```css
TaskExecutor挂掉了，CallbackHandler两次接受到回调发现Container是异常退出，会立即申请新的Container，pending container request置3(Container还没有启动TaskExecutor时，事实上Slot manager里的Slot是空的)
任务重启申请了6个Slot，Slot Manager会重新向Flink。Resource Manager并申请3个Container，pending container request置6
结果是6个Container比配置多了一倍，6个Container提供了12个Slot，但实际运行的Slot只有6个，另外6个Slot是闲置，也不会去回收
```

解决方案

```css
尝试解决方案1：接受到容器退出通知时不申请新容器，等任务重启时，向Slot Manager申请Slot时再去申请新的容器，会造成另外一个问题：当TaskExecutor启动报错时退出了，事实上从来没有注册Slot，TaskExecutor通知CallbackHandler，CallbackHandler也没任务作为，2个Slot request一直积压，永远得不到满足

尝试解决方案2：Flink ResourceManager在申请container之前检查下Pending Slot
Ex. Pending Slot是6，pending request container当是3正好满足需求，当>3是超出需求，且多出的会造成闲置
```

修复情况

```css
1.5.1 1.6.0版本中修复
另一个patch需要手动打，参考Flink issue 9567

1.6.2和1.5.5中完全修复
```

### (2)延时监控

一个简单的任务图：2个Resource、2个算子operator、2个并行度
延时监控数据计算：每个Resource子任务 每个算子的子任务 2个算子之间的延迟
$N = n_{(subtasks per source) }* n_{(source)} * n_{(subtasks per operator) }* n_{(operator)}$
假source和算子的并行度都为p，可简化为 $N = p^2 * n_{source} * n_{(operator)} $
2个source，2个除了source以外的operator，10个并行度，会收到400条延迟相关的消息。
有一个用户在Mailing List里反馈，开启latency tracking之后JobMaster很快就会挂掉。
24000+  1.6G+(存储监控数据的ConcurrenceHashMap)
开Application Master一般配置2G，光延迟相关的监控就占用了1.6G，不能容忍



解决方案一：关掉延迟监控，但无法感知到任务的延迟，也无法针对延迟去做监控
解决方案二：
Flink-10243 配置监控的粒度(不再测从每一个source的子任务到每一个算子的子任务之间的延迟，只测每个算子所有消息进来的延迟是多少)，从源头上减少监控的数量
$N_single = n_{subtasks per operator} * n_{(operator)} $  400 => 20
Flink-10246 改进的MetricQueryService
Flink-10247 & Flink-10253 & Flink-10602:为监控相关的服务建立一个低优先级的ActorSystem，防止影响主要组件
Flink-10252 reviewing：控制监控消息的大小

### (3)用户代码中启用SpringContext，在Task执行过程中去获取Bean

本身就不在同一个JVM，肯定获取不到

### (4)在实际执行function的open方法中通过配置文件获取SpringContext

一个TaskManager有3个Task Slot，每个Task Slot都可能会启动一个SpringContext，因一个JVM启动2个SpringContext会出问题

一个TaskManager只启一个Task Slot也不行，OperationChain会将窄依赖的算子嵌到一个Operator中

CoLocationGroup会把几个Sub Task放到一个Task Slot中去执行，这样优化并行度

解决方案：

封了单例的SpringContext，在算子的open方法中获取这个单例来获取相应的Bean

### (5)用Dubbo服务的吞吐

一个Dubbo服务调用10ms-500ms，吞吐量限制在100

多次调用返回同一个值做缓存

考虑异步去做提升吞吐量，实际Flink异步不支持KeyedState

RichAsyncFunction不支持使用Flink KeyedState

方法一：将缓存放到heap中做LRU cache，就没办法利用到Flink对state的管理能力

方法二：改变KeyedState的指向，继承AbstractRichFunction，实现AsyncFunction

# Spark

尽可能避免使用 reduceByKey、join、distinct、repartition 等会进行 shuffle 的算子，尽量使用 map 类的非 shuffle 算子

**Spark**基于**RDD  r**educe产生 shuffle 数据可缓存在内存，Hadoop 每次 shuffle 后必须写到磁盘

Hadoop 每次 MapReduce 启动一个 Task 便会启动一次 JVM

Spark 每次 MapReduce是基于线程，只在启动 Executor 是启动一次 JVM，内存的 Task可线程复用

DAG描述了 RDD 的依赖lineage血缘关系，2类，

action（触发真正的作业提交，计算返回一个值给 Driver 程序） 和 transformation（不会立即触发作业提交，每一个 transformation 返回一个新的 RDD）

窄依赖的 RDD 在同一个 stage 中进行计算

RDD 只读的分区记录集合 RDD 有多少个 partition，就会产生多少个 task

窄依赖 一子一亲  每一个 parent RDD 的 partition 最多被子 RDD 的一个 partition 使用

宽依赖 多子一亲

DAGScheduler 会将 Job划分为多个 stage，然后每个 stage 创建一个 TaskSet

Executor 上有线程池，每接收到一个 Task，就用 TaskRunner 封装，然后从线程池里取出一个线程执行这个 task。

(TaskRunner 将我们编写的代码，拷贝，反序列化，执行 Task，每个 Task 执行 RDD 里的一个 partition)

Dataset 支持静态类型分析所以在 compile time 就能报错，各种 combinators（map，foreach 等）性能会更好

ML面向 Dataset[Row]、**MLLib** 是面对 RDD

Why：Yarn多用户下重用空闲CPU executor，standalone适合单用户？除了 Spark调度服务还提供调度，如 Hadoop MapReduce, Hive 

**Spark Streaming**小文件：

Spark Streaming 1batch作为1rdd

Spark Streaming 是无法动态调整并行度

Storm Topology可动态地调整并行度

## Spark 3.0支持7种join

```css
INNER JOIN(没有指定任何类型，默认是INNER JOIN)
CROSS JOIN(Cartesian Product笛卡尔积返回m*n，生产环境建议禁用)
LEFT OUTER JOIN(等价于LEFT JOIN)
RIGHT OUTER JOIN
FULL OUTER JOIN
LEFT SEMI JOIN
LEFT ANTI JOIN
```

# MySQL Oracle(去IOE)

## 连接池 

DBCP, C3P0, BoneCP, Druid(凯尔特人的祭司), HikariCP(Hikari日语中是光的意思，像光一样快)

## 数据库排序算法

```css
http://wwwlgis.informatik.uni-kl.de/archiv/wwwdvs.informatik.uni-kl.de/courses/DBSREAL/SS2005/Vorlesungsunterlagen/Implementing_Sorting.pdf

(1)Files-Sorting/Searching
(2)Access Methods
(3)Query processing
(4)File organization
```

```css
Virtually all database products employ external merge-sort algorithm for query processing and index creation.

Query operations with efficient sort-based algorithms include duplicate removal, verifying uniqueness, rank and top operations, grouping, roll-up and cube operations, and
merge-join. Minor variations of merge-join exist for outer join, semijoin, intersection,
union, and difference.

```



## MySQL>=5.7(2020-10-21 已发布8.0版本) Oracle  >= 11g数据库规范

```css
不允许on commit刷新模式，须使用on demand刷新。
context命名规则为系统名+子系统名+功能描述。 
delete或update禁止出现order by，防止DML出现不必要排序。
delete或update必须出现where子句，防止DML过程出现全表锁。
隐式转换，在查询列上发生隐式转换。禁止嵌套select子句，防止出现select子句的嵌套子查询，出现性能问题。
禁止出现重复查询子句，可以使用with as替换子句来提升SQL语句执行效率。
单个SQL文本长度不能超过4000字节。
高频未使用绑定变量<= 50个sql文本，单个sql中的绑定变量不要超过50。

# 授权
只能授权应用表查询权限给DEV角色。
只能授权EXECUTE 查询权限给EXEC角色。禁止授权给PUBLIC用户。

# 版本
sql分版本维护，不同版本建立不同的包，格式：系统号-版本号-序列号-表名-DML\DDL\Trigger\View.sql。package命名规则是：系统名+子系统名+功能描述。

# with check option
使用WITH CHECK OPTION 选项进行数据约束时，必须使用指定的约束名称。视图只操作它可以查询出来的数据，对于它查询不出的数据，即使基表有，也不可以通过视图来操作。（1）对于update，有with check option，要保证update后，数据要被视图查询出来（2）对于delete，有无with check option都一样（3）对于insert，有with check option，要保证insert后，数据要被视图查询出来（4）对于没有where 子句的视图，使用with check option是多余。
本地视图禁止使用超过一层的嵌套视图，远端视图禁止使用超过2层的嵌套视图。创建视图时禁止使用select * from表名 语句，要求将用到的字段在视图或查询语句中列明，防止增加字段对应不上代码实体类DTO、PO报错。 

# 建表
范式（一.列 二.消除单表PK依赖，单表主键多个选用业务无关的字段做主键 三、消除PK传递依赖，如电商商品表细分为商品简略信息和详情两张表）
除临时表、日志表，其他建表必须有数据创建人 varchar2(100) not null、创建时间 date not null、修改人varchar2(100) not null、修改时间四个字段date not null，时间类字段的值推荐通过Trigger方式实现，如update t set date = sysdate，不推荐通过程序代码实现new Date存入。特殊配置项源数据表一次性导入后再无更新或追加数据的操作可不加。
表中一行记录所有字段的长度不能超过改数据库的db_block_size大小。
表和字段必须有comment注释，对于type类型字段必须罗列所有枚举值及相应的业务含义。命名中不允许出现数据库的关键字Reserved Word。为避免大小写敏感，禁止使用双引号将对象引用。Date类型字段必须以date作为前缀或后缀，boolean类型的字段必须以is作为前缀，主键字段命名不能包含任何业务含义，可以采用命名规则：id\_表名或直接id、pk。索引命名格式：IX\_字段名或字段名组合（复合索引）
选PK的原则（1）PK永不为空（2）PK永不改变，禁止程序Update PK（3）PK本身不是识别值（4）选择单一字段做PK。建主键和建表语句必须分开写。创建主键必须创建索引，再创建主键，所有外键上都必须创建索引，不推荐创建外键方式关联表。唯一键创建方式与主键相同，先建索引，后加主键。禁止更新主键列值，不允许有SQL更新主键。
创建、更改或删除Table时必须带上属主的名字。建主键和索引不需要指定索引表空间。创建或删除Trigger时必须带上属主的名字。创建或删除view时必须带上属主的名字。修改表时，若有增加default值的列或者修改字段的非空属性，必须先做DDL增加字段，再做DDL修改增加字段的default值属性，然后再做DML更新，最后加非空属性。Trigger命名：行级为同名表的命名规则|_suffix，语句级为同表名的命名规则\_s\_suffix。可选的suffix包括：BI、BU、BD、BSH、BDB、AI、AU、AD、ASH、ADB、II、IU、ID、ISH、IDB。
表命名规则禁止表名中使用无效的prefix 如 tbl_、db_ 。创建主键、约束和索引，不能指定索引表空间。创建或删除索引必须带上表名和属主名如 phwww.TABLE_NAME 。 
字段精度要求、财务系统金额相关都用decimal

# view
删除物化视图时，如果是快速刷新的物化视图，需要同时删除物化视图日志。物化视图必须以mv结尾，格式：表名\_功能描述\_mv。
视图禁止order by，不允许使用force refresh。

# sequence
创建sequence(一般做PK)时，maxValue后面的值必须是9。创建或删除sequence时必须带上属主名字。所有的sequence必须使用cache，cache值必须最低为40。sequence的命名规则是：系统名\_子系统名\_功能名。所有sequence需使用no order选项，创建sequence必须制定maxvalue、minvalue、start with、increment by、cache的值。

# partition
分区是水平扩展，一个表最多有1024个分区。
分区类型有range分区，list分区，hash分区，key分区。
表分区必须命名，一般根据日期、地域分区归档数据。表分区命名格式为，表名+分区特征+pt，索引分区命名格式为索引名+分区特征+pi，采用Hash自动分区或Oracle 11g Interval分区后，系统自动生成的SYS开头的表分区和索引分区可以例外。分区越多，Oracle维护成本越高。非Hash分区不要超过32个分区，Hash分区不要超过64个分区。分区的目的是性能优化或数据管理、数据归档、大批量数据的删除，在解决其中的一个需求前提下，且表数据量大于2G，才考虑分区。使用列表分区时，分区中必须包含default分区。使用hash分区时，分区数必须是2的N次方。分区表索引设计（1）若分区列是索引列的子集（无论是prefix或non-prefix），则建立local index。否则，遵循（2）。（2）若索引是唯一的，则建立global index，否则遵循（3）。（3）若基于性能考虑，且OLTP应用，用户要求更快响应时间，则建立global index；若应用是DSS类型，则用户更注重吞吐量，则建立local index。若基于维护性更方便，则建立local index。分区设计需关注，最终的数据要均匀分布到每个分区，偏大或偏小的比例不超过15%。除全局临时表和logtmp用户下的业务临时表及日志表以外，其他表必须建立主键。一个索引包含的所有字段的最大长度必须<= （db_block_size-192)*60%。
使用范围分区和列表分区必须使用Enable row movement.

# 同义词
创建同义词时禁止使用or replace关键字，create table语句参数不能包含storage选项，在archivelog模式下不能包含no logging选项，nologging会影响数据库的灾备和恢复。必须使用公共同义词，不能使用私有同义词。删除不再使用的数据库对象时，必须删除关联的同义词。同义词命名名称必须与指向对象的名称同名。
所有可以被引用的对象都应该建同义词。

# 大表
大表修改索引时加online（ MySQL 5.6）不阻塞DML语句，不加会阻塞其他session DML，高频SQL打满CPU。大表默认值加not null，事务型SQL都不适合for update和parallel，宽表要分段插入，字段>400以上是宽表，若批量如insert all 插入的字段时绑定临时变量值要分段插入，字段数目要<400，或者说宽表插入不适合关系型数据库来做，避免高并发sql超过2的32次方，数据库直接挂掉。
电商宽表高并发，先保证核心流程涉及到的字段抽离建小表，剩余字段放大表异步同步，保证核心业务不受影响。
join on条件复合索引，要防null (null会导致数据倾斜) 或者 on null == null(条件缺失或无其他明显区分占比的条件时导致全表扫)，会使数据库宕机。
高并发SQL，空值传入在绑定变量时mybatis需强制指定字段的数据类型或if标签判空。select全表的要加条数限制，where 1=1这种小心 1=1的后面条件是否失效。
笛卡尔积的sql一定要尽量使索引index type类型为const常量，不能大表全表扫，前后表的数据都要尽可能小，高频sql越小越好，不经常变更数据不放库，放配置或放缓存。放库放缓存只是保存的时间不一样，单机缓存是CP，集群缓存是AP，有读写和频繁更新缓存最终要刷盘落库，防止串状态。
大表禁select … insert into…，可采用匿名块、cursor进行批次处理，并记录log优化。

# explain
嵌套连接过深，执行计划中不允许嵌套过深超过6层。全表扫描，对于大于200M的表全表扫描，执行计划有TABLE ACCESS FULL操作，高频全表扫，表大小超过200M，且高频SQL如15分钟执行500次，PIR 3 Peak Information Rate级，表大小超过高速缓存1.5%，PIR 2级。
索引跳跃，执行计划中存在INDEX FULL SCAN

# 缓存
MySQL select会缓存查询结果，key是SQL语句，value是查询结果，是否开启缓存 query_cache_type，大小设定query_cache_size

# 函数
like 'xx%'走索引的通配查询优化，比如客户表查找以.com结尾的电子邮件， select  XX from T where email like '%.com'改为REVERSE('%.com')	ex. mysql> select REVERSE('abc');  -> 'cba'。思考like '%xx'为啥不走索引？
字符串偏向数值思想，INET_ATON(IP) 把 ip 转换为数字 Ex.查ip 在 192.168.1.3 到 192.168.1.20 之间的记录
select * from ip_table where inet_aton(ip) > inet_aton('192.168.1.3') and inet_aton(ip) < inet_aton('192.168.1.20');

# 关联
A表20W数据，B表500W数据，关联条件的字段建立索引，相互索引效率更高，一般小表 left join 大表效率更高些

# 索引Type类型
type类型字段尽量 2的n次方如2、4、8、16，避免1、2、3、4这种，最好not null带默认值，最好是数值型而不是varcach2类型，避免隐式转换。不追求性能可以存大写枚举字符串、前后端交互、数据库实体可以枚举交互

# NULL数据倾斜和影响
NULL对索引的影响、索引列尽量不为NULL，表设计比较忌讳`NULL`不能使用=、<、>这样的运算符，对null做算术运算的结果都是null。count(col)不会包括null行等，但count(*)会被优化，总是直接返回总行数的。null比空字符串需要更多的存储空间。
往timestamp类型的列中插入NULL值，插入的是系统当前时间。往auto_increment属性的列中插入NULL，会插入一个正整数。往字符型的列中插入NULL，插入的就是NULL。

#MySQL date类型
对于按天统计的需求可以用友好冗余date类型字段设计，date类型受时区影响 
查看数据库时区 show variables like "%time_zone%";

临时更改MySQL时区  
# 设置全局时区 mysql> set global time_zone = '+8:00';
Query OK, 0 rows affected (0.00 sec) 
# 设置时区为东八区 mysql> set time_zone = '+8:00'; 
Query OK, 0 rows affected (0.00 sec) 
# 刷新权限使设置立即生效 mysql> flush privileges; 
Query OK, 0 rows affected (0.00 sec)

永久修改MySQL时区
vi /etc/mysql/my.cnf
# 增加
default-time_zone = '+8:00'
# 重启
service mysql restart

应用配置相关
# 时区设置   返回给前端的时间格式和时区设定，保证前端页面显示时间和数据库一致
spring.jackson.time-zone=GMT+8
# 时间格式  
spring.jackson.date-format=yyyy-MM-dd HH:mm:ss 
#Druid数据源配置  设置数据库时间为东八区（北京）时间，保证debug时候从数据库查出时间一致
spring.datasource.url= ****************** &serverTimezone=Asia/Shanghai
```

## 设计

### SQL自动检查

Yearning MYSQL

### SQL优化点

SQL语句（效果小）、索引、字段、表设计、主从复制（MySQL replicate）、读写分离（Ex. a.javax.sql.connection WriteDatabase ReadDatabase b.Spring AOP和Aspect实现数据源动态切换）、HA（双备）

```css
(1)定长与非定长对limit影响？
分页最好不要让别人看到10W条以后的数据，即使用了索引，百万级分页也是极限，一百多万的数据用id in (str)很快

SELECT column FROM table LIMIT 1000000, 10; 分页会很慢，数据库找第1000000条记录的开始id会花费很多时间 SELECT column FROM table ORDER BY id LIMIT 1000000, 10;加了PK索引会稍微快一点 
优化 SELECT column FROM table WHERE id >= (SELECT id FROM table LIMIT 1000000, 1) LIMIT 10; 
或进一步优化 SELECT column FROM table WHERE id BETWEEN 1000000 AND 1000010;

(2)查询id不是连续的一段，最佳方法是先找到id，再用in查询
SELECT * FROM table WHERE id IN(10000, 100000, 1000000...);

(3)查询一段较长字符串时，表设计时要多加一字段如对网址的CRC32或MD5，查询时不要直接查字符串而是查CRC32或MD5

(4)前缀索引
前缀索引一般只能用于普通索引，不能使用在unique
前缀索引只支持英文和数字
作用是优化索引的存储空间，查询速度
有点类似Oracle中对字段使用left()，建立函数索引；MySQL的前缀索引在查询时是内部自动完成匹配，并不需要使用left()
前缀索引局限：order by, group by, 覆盖索引Covering Index就无法使用
语法是ALTER TABLE table_name ADD KEY(column_name(prefix_length));

Ex. 
-- 整字段索引选择性Index Selectivity 0.0042
select count(distinct first_name) / count(1) from employees; 

-- first_name 前几个字符串的索引选择性Index Selectivity 5:0.0037;  6:0.0041;  7:0.0042;  8:0.0042，可以看出first_name的前缀索引定在了7个字符串，alter table employees add key (first_name(7));
select count(distinct left(employees.first_name, 5)) / count(1)
from employees;
MySQL没有后缀索引，但可以牺牲空间来换，冗余 first_name_reverse 字段存first_name reverse后的值，对first_name_reverse创建前缀索引，等价于实现了一个first_name后缀索引

(5)Covering Index覆盖索引
-- 数据75W条
Ex.CREATE TABLE `user_group` (
  `id` int(11) NOT NULL auto_increment,
  `uid` int(11) NOT NULL,
  `group_id` int(11) NOT NULL,
  PRIMARY KEY  (`id`),
  KEY `uid` (`uid`),
  KEY `group_id` (`group_id`),
) ENGINE=InnoDB AUTO_INCREMENT=750366 DEFAULT CHARSET=utf8;

SELECT SQL_NO_CACHE uid FROM user_group WHERE group_id = 245;
+----+-------------+------------+------+---------------+----------+---------+-------+------+-------+
| id | select_type | table      | type | possible_keys | key      | key_len | ref   | rows | Extra |
+----+-------------+------------+------+---------------+----------+---------+-------+------+-------
|  1 | SIMPLE      | user_group | ref  | group_id      | group_id | 4       | const | 5544 |       |
+----+-------------+------------+------+---------------+----------+---------+-------+------+-------

ALTER TABLE user_group ADD INDEX group_id_uid (group_id, uid);
+----+-------------+------------+------+-----------------------+--------------+---------+-------+----
| id | select_type | table      | type | possible_keys         | key          | key_len | ref   | rows | Extra       |
+----+-------------+------------+------+-----------------------+--------------+---------+-------+--

|  1 | SIMPLE      | user_group | ref  | group_id,group_id_uid | group_id_uid | 4       | const | 5378 | Using index |
+----+-------------+------------+------+-----------------------+--------------+---------+-------+--
覆盖索引Covering index, MySQL只需通过索引就可以返回查询所需要的数据，而不必在查到索引之后再去查数据。
但同时要求所查询的字段必须被索引所覆盖到，在Explain时，输出的Extra若有Using Index则表示这条查询用了覆盖索引 Covering index

(6) SQL_NO_CACHE
SELECT SQL_NO_CACHE column FROM table WHERE id = 1;

混合排序
https://www.jianshu.com/p/591e15374d09
```

## MySQL crash recovery

非正常关闭（数据库实例crash、服务器crash）导致错误日志

正常关闭，所有buffer pool里的脏页都会刷新一遍到磁盘，同时记录最新LSN到ibdata文件第一个page中；而非正常关闭来不及做这些操作，即没及时将脏数据flush到磁盘，也没有记录最新LSN到ibdata file

重启数据库实例时，做2个二阶段：redo log操作，undo log及bin log处理

```mysql
[Note] InnoDB: Database was not shutdown normally!
[Note] InnoDB: Starting crash recovery.
[Note] InnoDB: Reading tablespace information from the .ibd files...
[ERROR] InnoDB: Attempted to open a previously opened tablespace. Previous tablespace sakila/cou
ntry uses space ID: 32 at filepath: ./sakila/country.ibd. Cannot open tablespace wordpress/wp_options which uses space ID
: 32 at filepath: ./wordpress/wp_options.ibd
 7f9868b4e780 InnoDB: Operating system error number 2 in a file operation.
InnoDB: The error means the system cannot find the path specified.
InnoDB: If you are installing InnoDB, remember that you must create
InnoDB: directories yourself, InnoDB does not create them.
InnoDB: Error: could not open single-table tablespace file ./wordpress/wp_options.ibd
InnoDB: We do not continue the crash recovery, because the table may become
InnoDB: corrupt if we cannot apply the log records in the InnoDB log to it.
InnoDB: To fix the problem and start mysqld:
InnoDB: 1) If there is a permission problem in the file and mysqld cannot
InnoDB: open the file, you should modify the permissions.
InnoDB: 2) If the table is not needed, or you can restore it from a backup,
InnoDB: then you can remove the .ibd file, and InnoDB will do a normal
InnoDB: crash recovery and ignore that table.
InnoDB: 3) If the file system or the disk is broken, and you cannot remove
InnoDB: the .ibd file, you can set innodb_force_recovery > 0 in my.cnf
InnoDB: and force InnoDB to continue crash recovery here.
```

```css
解决方案：
(1)在my.cnf中添加以下参数
在[mysqlId]组中加入 innodb_force_recovery=6 后启动MySQL

innodb_force_recovery影响整个InnoDB恢复状况，默认值为0，表示当需要恢复时执行所有的恢复操作。
当不能进行有效的恢复操作时，MySQL有可能无法启动，并记录下错误日志。

innodb_force_recovery可以设置为1-6,大的数字包含前面所有数字的影响。
当设置参数值大于0后，允许对表select,create,drop,但不允许insert,update或者delete。

说明：
1(SRV_FORCE_IGNORE_CORRUPT):忽略检查到的corrupt页
2(SRV_FORCE_NO_BACKGROUND):阻止主线程的运行，如主线程需要执行full purge操作，会导致crash
3(SRV_FORCE_NO_TRX_UNDO):不执行事务回滚操作。
4(SRV_FORCE_NO_IBUF_MERGE):不执行插入缓冲的合并操作。
5(SRV_FORCE_NO_UNDO_LOG_SCAN):不查看重做日志，InnoDB存储引擎会将未提交的事务视为已提交。
6(SRV_FORCE_NO_LOG_REDO):不执行前滚的操作。
(2)备份
mysqldump SECHMANAME > BackUpXX.sql
(3)删物理文件
(4)重启MySQL
(5)导入备份BackUpXX.sql
原库SECHMANAME无法导入提示已存在，手动删除后导入还提示idb文件已存在
但导入其他库正常，修改配置文件里的数据库为新库，之后重新授权新库
```

## binlog

```css
Server层日志系统，binlog中跟踪对数据库的所有更改操作，是逻辑日志，以追加日志的形式记录。

三种格式：(1)statement (2)row (3)mixed

statement记录SQL语句原文，风险点是若主从用到的索引不同，操作带limit时，处理可能时不同行的记录数据
row仅记录某条记录数据修改细节，不关系上下文，缺陷占用空间，同时写binlog很耗IO，影响执行速度
mixed一般语句使用statement保存，若使用了函数，statement无法完成主从复制，采用row格式。MySQL会判断SQL语句是否可能引起主备不一致，有则用row，否则用statement
```

### 开启binlog

```css
[mysqld] 
     ...... 
     log_bin = mysql_bin 
     ...... 
     // log_bin是生成的bin-log的文件名，后缀则是6位数字编码，从000001开始，生成的文件则为： 
     mysql_bin.000001 
     mysql_bin.000002 
 配置保存后重启MySQL，show variables like '%bin%';查看bin-log是否开启看参数log_bin是否是ON？
```

### Kafka binlog全局有序

```java
// Kafka消息如何选择计算 Partition 源码
/**
 * The default partitioning strategy:
 * <li>If a partition is specified in the record, use it
 * <li>If no partition is specified but a key is present choose a partition based on a hash of the key
 * <li>If no partition or key is present choose a partition in a round-robin fashion
 */
public class DefaultPartitioner implements Partitioner {

    private final ConcurrentMap<String, AtomicInteger> topicCounterMap = new ConcurrentHashMap<>();

    public void configure(Map<String, ?> configs) {}

    /**
     * Compute the partition for the given record.
     *
     * @param topic The topic name
     * @param key The key to partition on (or null if no key)
     * @param keyBytes serialized key to partition on (or null if no key)
     * @param value The value to partition on or null
     * @param valueBytes serialized value to partition on or null
     * @param cluster The current cluster metadata
     */
    public int partition(String topic, Object key, byte[] keyBytes, Object value, byte[] valueBytes, Cluster cluster) {
        List<PartitionInfo> partitions = cluster.partitionsForTopic(topic);
        int numPartitions = partitions.size();
        if (keyBytes == null) {
            int nextValue = nextValue(topic);
            List<PartitionInfo> availablePartitions = cluster.availablePartitionsForTopic(topic);
            if (availablePartitions.size() > 0) {
                int part = Utils.toPositive(nextValue) % availablePartitions.size();
                return availablePartitions.get(part).partition();
            } else {
                // no partitions are available, give a non-available partition
                return Utils.toPositive(nextValue) % numPartitions;
            }
        } else {
            // hash the keyBytes to choose a partition
            return Utils.toPositive(Utils.murmur2(keyBytes)) % numPartitions;
        }
    }

    private int nextValue(String topic) {
        AtomicInteger counter = topicCounterMap.get(topic);
        if (null == counter) {
            counter = new AtomicInteger(ThreadLocalRandom.current().nextInt());
            AtomicInteger currentCounter = topicCounterMap.putIfAbsent(topic, counter);
            if (currentCounter != null) {
                counter = currentCounter;
            }
        }
        return counter.getAndIncrement();
    }

    public void close() {}

}

```



```css
Kafka中每个partition数据都是有序，数据发送到某topic内全局数据是乱序

生产上producer.send消息到kafka，指定key，根据key hash求出一个固定分区确保相同key发送到同一个partition，可根据某个topic，指定某一个partition

topic默认是3个partition
架构：MySQL binlog ---> Canal ---> Kafka ---> Flink ---> Kudu
Canal抽取MySQL binlog写入Kafka

Kafka有个名为T1的topic，T1有3个partition
T1执行一波操作Op1：i, u1, u2, u3, u4, d (i=insert, u=update, d=delete, Op=operation)

不保证全局有序结果：
p0：u1, u4 (p=partition)
p1: i, u2
p2: u3, d
下游Kafka消费是错误顺序

解决方案：
(1)topic只设置一个partition，牺牲性能和存在数据量提升隐患，所有数据都发往同一个partition
(2)下游消费者对topic做分组时间排序，性能也差
(3)特征数据处理
producer.send(new ProducerRecord<>(topic,messageNo,messageStr))
messageNo = database.table.key 如操作Op1 key为id = 100，则messageNo=bigdata.T1.100
计算partition 假设hash(bigdata.T1.100)=99
99%3=0对应p0

数据操作Op1分发到p0分区：
p0：i u1 u2 u3 u4 d
p1:
p2:

如bigdata.t2.666 发送到了p1
p0：
p1: i u1 u2 u3 u4 d
p2:
```

### binlog缓存问题

```css
错误日志(1)：
Last_SQL_Errno: 1197
Last_SQL_Error: Worker 14 failed executing transaction '' at master log mysql-bin.050101, end_log_pos 2669492980; Could not execute Delete_rows_v1 event on table time_dispatcher_0029.ttd_task_1889; Multi-statement transaction required more than 'max_binlog_cache_size' bytes of storage; increase this mysqld variable and try again, Error_code: 1197; handler error HA_ERR_RBR_LOGGING_FAILED; the event's master log mysql-bin.050101, end_log_pos 2669492980

解决方案(1)：
show variables like '%binlog_%size%';
show status like 'binlog_%';  
show variables like '%binlog_cache_size%';
查看主、从机器的cache大小设置是否相同，修改命令是set global max_binlog_cache_size=10737418240(具体值要主从保持一致);    
```

```css
错误日志(2)：
ERROR 1197 (HY000): Multi-statement transaction required more than 'max_binlog_cache_size' bytes of storage;max_binlog_cache_size最低值是4096，最大可能值为16EB(艾字节)

Note:
Prior to MySQL 5.6.7, 64-bit Windows platforms truncated the stored value for this variable max_binlog_cache_size to 4G, even when it was set to a greater value (Bug #13961678).
```

### show binlog events;

```mysql
mysql> show binlog events in 'mysql-bin.000224' limit 3,5; 从第3行开始列出5行；
# /usr/local/mysql/bin/mysqlbinlog mysql-bin.000220 |  grep -A10 "at 764$"
```

### 利用bin_log恢复数据

```css
mysqlbinlog  --start-date="2012-10-15 16:30:00" --stop-date="2012-10-15 17:00:00" mysql_bin.000001 | mysql -uroot -p123456 

--start-positon="50"  // 指定从50位置开始 
--stop-postion="100"  // 指定到100位置结束 
```

### Canal

```css
Canal基于MySQL增量日志解析，提供增量数据订阅和消费。
Canal支持源端 MySQL 版本5.1.x , 5.5.x , 5.6.x , 5.7.x , 8.0.x

1.MySQL master将数据变更写入二进制Binary log，记录二进制日志事件binary log events，可通过show binlog events;进行查看
2.MySQL slave将master binary log events 拷贝到中继日志 relay log
3.MySQL slave重放 relay log事件
```



MySQL information_schema

```sql
-- '5.7.30'
select version();

use information_schema;
show tables;
select * from INFORMATION_SCHEMA.TABLES where TABLE_NAME = 'budget';
```



| Tables\_in\_information\_schema          |      |
| :--------------------------------------- | ---- |
| CHARACTER\_SETS                          |      |
| COLLATIONS                               |      |
| COLLATION\_CHARACTER\_SET\_APPLICABILITY |      |
| COLUMNS                                  |      |
| COLUMN\_PRIVILEGES                       |      |
| ENGINES                                  |      |
| EVENTS                                   |      |
| FILES                                    |      |
| GLOBAL\_STATUS                           |      |
| GLOBAL\_VARIABLES                        |      |
| KEY\_COLUMN\_USAGE                       |      |
| OPTIMIZER\_TRACE                         |      |
| PARAMETERS                               |      |
| PARTITIONS                               |      |
| PLUGINS                                  |      |
| PROCESSLIST                              |      |
| PROFILING                                |      |
| REFERENTIAL\_CONSTRAINTS                 |      |
| ROUTINES                                 |      |
| SCHEMATA                                 |      |
| SCHEMA\_PRIVILEGES                       |      |
| SESSION\_STATUS                          |      |
| SESSION\_VARIABLES                       |      |
| STATISTICS                               |      |
| TABLES                                   |      |
| TABLESPACES                              |      |
| TABLE\_CONSTRAINTS                       |      |
| TABLE\_PRIVILEGES                        |      |
| TRIGGERS                                 |      |
| USER\_PRIVILEGES                         |      |
| VIEWS                                    |      |
| INNODB\_LOCKS                            |      |
| INNODB\_TRX                              |      |
| INNODB\_SYS\_DATAFILES                   |      |
| INNODB\_FT\_CONFIG                       |      |
| INNODB\_SYS\_VIRTUAL                     |      |
| INNODB\_CMP                              |      |
| INNODB\_FT\_BEING\_DELETED               |      |
| INNODB\_CMP\_RESET                       |      |
| INNODB\_CMP\_PER\_INDEX                  |      |
| INNODB\_CMPMEM\_RESET                    |      |
| INNODB\_FT\_DELETED                      |      |
| INNODB\_BUFFER\_PAGE\_LRU                |      |
| INNODB\_LOCK\_WAITS                      |      |
| INNODB\_TEMP\_TABLE\_INFO                |      |
| INNODB\_SYS\_INDEXES                     |      |
| INNODB\_SYS\_TABLES                      |      |
| INNODB\_SYS\_FIELDS                      |      |
| INNODB\_CMP\_PER\_INDEX\_RESET           |      |
| INNODB\_BUFFER\_PAGE                     |      |
| INNODB\_FT\_DEFAULT\_STOPWORD            |      |
| INNODB\_FT\_INDEX\_TABLE                 |      |
| INNODB\_FT\_INDEX\_CACHE                 |      |
| INNODB\_SYS\_TABLESPACES                 |      |
| INNODB\_METRICS                          |      |
| INNODB\_SYS\_FOREIGN\_COLS               |      |
| INNODB\_CMPMEM                           |      |
| INNODB\_BUFFER\_POOL\_STATS              |      |
| INNODB\_SYS\_COLUMNS                     |      |
| INNODB\_SYS\_FOREIGN                     |      |
| INNODB\_SYS\_TABLESTATS                  |      |

| TABLE\_CATALOG | TABLE\_SCHEMA | TABLE\_NAME | TABLE\_TYPE  | ENGINE | VERSION | ROW\_FORMAT | TABLE\_ROWS | AVG\_ROW\_LENGTH | DATA\_LENGTH | MAX\_DATA\_LENGTH | INDEX\_LENGTH | DATA\_FREE | AUTO\_INCREMENT | CREATE\_TIME            | UPDATE\_TIME            | CHECK\_TIME | TABLE\_COLLATION     | CHECKSUM | CREATE\_OPTIONS | TABLE\_COMMENT |
| -------------- | ------------- | ----------- | ------------ | ------ | ------- | ----------- | ----------- | ---------------- | ------------ | ----------------- | ------------- | ---------- | --------------- | ----------------------- | ----------------------- | ----------- | -------------------- | -------- | --------------- | -------------- |
| def            | ghxc\_ica     | budget      | "BASE TABLE" | InnoDB | 10      | Dynamic     | 1           | 16384            | 16384        | 0                 | 32768         | 0          | 3               | "2020\-10\-19 17:36:27" | "2020\-10\-20 15:11:12" | NULL        | utf8mb4\_general\_ci | NULL     |                 | 预算           |

## show variables

```mysql
show variables; 
-- 查看单个
show variables like '%binlog_cache_size%';
```



| Variable\_name                                               | Value                                                        |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| auto\_generate\_certs                                        | ON                                                           |
| auto\_increment\_increment                                   | 1                                                            |
| auto\_increment\_offset                                      | 1                                                            |
| autocommit                                                   | ON                                                           |
| automatic\_sp\_privileges                                    | ON                                                           |
| avoid\_temporal\_upgrade                                     | OFF                                                          |
| back\_log                                                    | 170                                                          |
| basedir                                                      | /usr/local/mysql/                                            |
| big\_tables                                                  | OFF                                                          |
| bind\_address                                                | \*                                                           |
| binlog\_cache\_size                                          | 32768                                                        |
| binlog\_checksum                                             | CRC32                                                        |
| binlog\_direct\_non\_transactional\_updates                  | OFF                                                          |
| binlog\_error\_action                                        | ABORT\_SERVER                                                |
| binlog\_format                                               | ROW                                                          |
| binlog\_group\_commit\_sync\_delay                           | 0                                                            |
| binlog\_group\_commit\_sync\_no\_delay\_count                | 0                                                            |
| binlog\_gtid\_simple\_recovery                               | ON                                                           |
| binlog\_max\_flush\_queue\_time                              | 0                                                            |
| binlog\_order\_commits                                       | ON                                                           |
| binlog\_row\_image                                           | FULL                                                         |
| binlog\_rows\_query\_log\_events                             | OFF                                                          |
| binlog\_stmt\_cache\_size                                    | 32768                                                        |
| binlog\_transaction\_dependency\_history\_size               | 25000                                                        |
| binlog\_transaction\_dependency\_tracking                    | COMMIT\_ORDER                                                |
| block\_encryption\_mode                                      | aes\-128\-ecb                                                |
| bulk\_insert\_buffer\_size                                   | 8388608                                                      |
| character\_set\_client                                       | utf8mb4                                                      |
| character\_set\_connection                                   | utf8mb4                                                      |
| character\_set\_database                                     | utf8mb4                                                      |
| character\_set\_filesystem                                   | binary                                                       |
| character\_set\_results                                      | utf8mb4                                                      |
| character\_set\_server                                       | latin1                                                       |
| character\_set\_system                                       | utf8                                                         |
| character\_sets\_dir                                         | /usr/local/mysql/share/charsets/                             |
| check\_proxy\_users                                          | OFF                                                          |
| collation\_connection                                        | utf8mb4\_general\_ci                                         |
| collation\_database                                          | utf8mb4\_general\_ci                                         |
| collation\_server                                            | latin1\_swedish\_ci                                          |
| completion\_type                                             | NO\_CHAIN                                                    |
| concurrent\_insert                                           | AUTO                                                         |
| connect\_timeout                                             | 10                                                           |
| core\_file                                                   | OFF                                                          |
| datadir                                                      | /usr/local/mysql/data/                                       |
| date\_format                                                 | %Y\-%m\-%d                                                   |
| datetime\_format                                             | "%Y\-%m\-%d %H:%i:%s"                                        |
| default\_authentication\_plugin                              | mysql\_native\_password                                      |
| default\_password\_lifetime                                  | 0                                                            |
| default\_storage\_engine                                     | InnoDB                                                       |
| default\_tmp\_storage\_engine                                | InnoDB                                                       |
| default\_week\_format                                        | 0                                                            |
| delay\_key\_write                                            | ON                                                           |
| delayed\_insert\_limit                                       | 100                                                          |
| delayed\_insert\_timeout                                     | 300                                                          |
| delayed\_queue\_size                                         | 1000                                                         |
| disabled\_storage\_engines                                   |                                                              |
| disconnect\_on\_expired\_password                            | ON                                                           |
| div\_precision\_increment                                    | 4                                                            |
| end\_markers\_in\_json                                       | OFF                                                          |
| enforce\_gtid\_consistency                                   | OFF                                                          |
| eq\_range\_index\_dive\_limit                                | 200                                                          |
| error\_count                                                 | 0                                                            |
| event\_scheduler                                             | OFF                                                          |
| expire\_logs\_days                                           | 0                                                            |
| explicit\_defaults\_for\_timestamp                           | OFF                                                          |
| external\_user                                               |                                                              |
| flush                                                        | OFF                                                          |
| flush\_time                                                  | 0                                                            |
| foreign\_key\_checks                                         | ON                                                           |
| ft\_boolean\_syntax                                          | "\+ \-><\(\)~\*:""&\|"                                       |
| ft\_max\_word\_len                                           | 84                                                           |
| ft\_min\_word\_len                                           | 4                                                            |
| ft\_query\_expansion\_limit                                  | 20                                                           |
| ft\_stopword\_file                                           | \(built\-in\)                                                |
| general\_log                                                 | OFF                                                          |
| general\_log\_file                                           | /usr/local/mysql/data/office\-UNION\-Dev\-07\.log            |
| group\_concat\_max\_len                                      | 1024                                                         |
| gtid\_executed\_compression\_period                          | 1000                                                         |
| gtid\_mode                                                   | OFF                                                          |
| gtid\_next                                                   | AUTOMATIC                                                    |
| gtid\_owned                                                  |                                                              |
| gtid\_purged                                                 |                                                              |
| have\_compress                                               | YES                                                          |
| have\_crypt                                                  | YES                                                          |
| have\_dynamic\_loading                                       | YES                                                          |
| have\_geometry                                               | YES                                                          |
| have\_openssl                                                | YES                                                          |
| have\_profiling                                              | YES                                                          |
| have\_query\_cache                                           | YES                                                          |
| have\_rtree\_keys                                            | YES                                                          |
| have\_ssl                                                    | YES                                                          |
| have\_statement\_timeout                                     | YES                                                          |
| have\_symlink                                                | DISABLED                                                     |
| host\_cache\_size                                            | 633                                                          |
| hostname                                                     | office\-UNION\-Dev\-07                                       |
| identity                                                     | 0                                                            |
| ignore\_builtin\_innodb                                      | OFF                                                          |
| ignore\_db\_dirs                                             |                                                              |
| init\_connect                                                |                                                              |
| init\_file                                                   |                                                              |
| init\_slave                                                  |                                                              |
| innodb\_adaptive\_flushing                                   | ON                                                           |
| innodb\_adaptive\_flushing\_lwm                              | 10                                                           |
| innodb\_adaptive\_hash\_index                                | ON                                                           |
| innodb\_adaptive\_hash\_index\_parts                         | 8                                                            |
| innodb\_adaptive\_max\_sleep\_delay                          | 150000                                                       |
| innodb\_api\_bk\_commit\_interval                            | 5                                                            |
| innodb\_api\_disable\_rowlock                                | OFF                                                          |
| innodb\_api\_enable\_binlog                                  | OFF                                                          |
| innodb\_api\_enable\_mdl                                     | OFF                                                          |
| innodb\_api\_trx\_level                                      | 0                                                            |
| innodb\_autoextend\_increment                                | 64                                                           |
| innodb\_autoinc\_lock\_mode                                  | 1                                                            |
| innodb\_buffer\_pool\_chunk\_size                            | 134217728                                                    |
| innodb\_buffer\_pool\_dump\_at\_shutdown                     | ON                                                           |
| innodb\_buffer\_pool\_dump\_now                              | OFF                                                          |
| innodb\_buffer\_pool\_dump\_pct                              | 25                                                           |
| innodb\_buffer\_pool\_filename                               | ib\_buffer\_pool                                             |
| innodb\_buffer\_pool\_instances                              | 1                                                            |
| innodb\_buffer\_pool\_load\_abort                            | OFF                                                          |
| innodb\_buffer\_pool\_load\_at\_startup                      | ON                                                           |
| innodb\_buffer\_pool\_load\_now                              | OFF                                                          |
| innodb\_buffer\_pool\_size                                   | 134217728                                                    |
| innodb\_change\_buffer\_max\_size                            | 25                                                           |
| innodb\_change\_buffering                                    | all                                                          |
| innodb\_checksum\_algorithm                                  | crc32                                                        |
| innodb\_checksums                                            | ON                                                           |
| innodb\_cmp\_per\_index\_enabled                             | OFF                                                          |
| innodb\_commit\_concurrency                                  | 0                                                            |
| innodb\_compression\_failure\_threshold\_pct                 | 5                                                            |
| innodb\_compression\_level                                   | 6                                                            |
| innodb\_compression\_pad\_pct\_max                           | 50                                                           |
| innodb\_concurrency\_tickets                                 | 5000                                                         |
| innodb\_data\_file\_path                                     | ibdata1:12M:autoextend                                       |
| innodb\_data\_home\_dir                                      |                                                              |
| innodb\_deadlock\_detect                                     | ON                                                           |
| innodb\_default\_row\_format                                 | dynamic                                                      |
| innodb\_disable\_sort\_file\_cache                           | OFF                                                          |
| innodb\_doublewrite                                          | ON                                                           |
| innodb\_fast\_shutdown                                       | 1                                                            |
| innodb\_file\_format                                         | Barracuda                                                    |
| innodb\_file\_format\_check                                  | ON                                                           |
| innodb\_file\_format\_max                                    | Barracuda                                                    |
| innodb\_file\_per\_table                                     | ON                                                           |
| innodb\_fill\_factor                                         | 100                                                          |
| innodb\_flush\_log\_at\_timeout                              | 1                                                            |
| innodb\_flush\_log\_at\_trx\_commit                          | 1                                                            |
| innodb\_flush\_method                                        |                                                              |
| innodb\_flush\_neighbors                                     | 1                                                            |
| innodb\_flush\_sync                                          | ON                                                           |
| innodb\_flushing\_avg\_loops                                 | 30                                                           |
| innodb\_force\_load\_corrupted                               | OFF                                                          |
| innodb\_force\_recovery                                      | 0                                                            |
| innodb\_ft\_aux\_table                                       |                                                              |
| innodb\_ft\_cache\_size                                      | 8000000                                                      |
| innodb\_ft\_enable\_diag\_print                              | OFF                                                          |
| innodb\_ft\_enable\_stopword                                 | ON                                                           |
| innodb\_ft\_max\_token\_size                                 | 84                                                           |
| innodb\_ft\_min\_token\_size                                 | 3                                                            |
| innodb\_ft\_num\_word\_optimize                              | 2000                                                         |
| innodb\_ft\_result\_cache\_limit                             | 2000000000                                                   |
| innodb\_ft\_server\_stopword\_table                          |                                                              |
| innodb\_ft\_sort\_pll\_degree                                | 2                                                            |
| innodb\_ft\_total\_cache\_size                               | 640000000                                                    |
| innodb\_ft\_user\_stopword\_table                            |                                                              |
| innodb\_io\_capacity                                         | 200                                                          |
| innodb\_io\_capacity\_max                                    | 2000                                                         |
| innodb\_large\_prefix                                        | ON                                                           |
| innodb\_lock\_wait\_timeout                                  | 50                                                           |
| innodb\_locks\_unsafe\_for\_binlog                           | OFF                                                          |
| innodb\_log\_buffer\_size                                    | 16777216                                                     |
| innodb\_log\_checksums                                       | ON                                                           |
| innodb\_log\_compressed\_pages                               | ON                                                           |
| innodb\_log\_file\_size                                      | 50331648                                                     |
| innodb\_log\_files\_in\_group                                | 2                                                            |
| innodb\_log\_group\_home\_dir                                | \./                                                          |
| innodb\_log\_write\_ahead\_size                              | 8192                                                         |
| innodb\_lru\_scan\_depth                                     | 1024                                                         |
| innodb\_max\_dirty\_pages\_pct                               | 75\.000000                                                   |
| innodb\_max\_dirty\_pages\_pct\_lwm                          | 0\.000000                                                    |
| innodb\_max\_purge\_lag                                      | 0                                                            |
| innodb\_max\_purge\_lag\_delay                               | 0                                                            |
| innodb\_max\_undo\_log\_size                                 | 1073741824                                                   |
| innodb\_monitor\_disable                                     |                                                              |
| innodb\_monitor\_enable                                      |                                                              |
| innodb\_monitor\_reset                                       |                                                              |
| innodb\_monitor\_reset\_all                                  |                                                              |
| innodb\_numa\_interleave                                     | OFF                                                          |
| innodb\_old\_blocks\_pct                                     | 37                                                           |
| innodb\_old\_blocks\_time                                    | 1000                                                         |
| innodb\_online\_alter\_log\_max\_size                        | 134217728                                                    |
| innodb\_open\_files                                          | 2000                                                         |
| innodb\_optimize\_fulltext\_only                             | OFF                                                          |
| innodb\_page\_cleaners                                       | 1                                                            |
| innodb\_page\_size                                           | 16384                                                        |
| innodb\_print\_all\_deadlocks                                | OFF                                                          |
| innodb\_purge\_batch\_size                                   | 300                                                          |
| innodb\_purge\_rseg\_truncate\_frequency                     | 128                                                          |
| innodb\_purge\_threads                                       | 4                                                            |
| innodb\_random\_read\_ahead                                  | OFF                                                          |
| innodb\_read\_ahead\_threshold                               | 56                                                           |
| innodb\_read\_io\_threads                                    | 4                                                            |
| innodb\_read\_only                                           | OFF                                                          |
| innodb\_replication\_delay                                   | 0                                                            |
| innodb\_rollback\_on\_timeout                                | OFF                                                          |
| innodb\_rollback\_segments                                   | 128                                                          |
| innodb\_sort\_buffer\_size                                   | 1048576                                                      |
| innodb\_spin\_wait\_delay                                    | 6                                                            |
| innodb\_stats\_auto\_recalc                                  | ON                                                           |
| innodb\_stats\_include\_delete\_marked                       | OFF                                                          |
| innodb\_stats\_method                                        | nulls\_equal                                                 |
| innodb\_stats\_on\_metadata                                  | OFF                                                          |
| innodb\_stats\_persistent                                    | ON                                                           |
| innodb\_stats\_persistent\_sample\_pages                     | 20                                                           |
| innodb\_stats\_sample\_pages                                 | 8                                                            |
| innodb\_stats\_transient\_sample\_pages                      | 8                                                            |
| innodb\_status\_output                                       | OFF                                                          |
| innodb\_status\_output\_locks                                | OFF                                                          |
| innodb\_strict\_mode                                         | ON                                                           |
| innodb\_support\_xa                                          | ON                                                           |
| innodb\_sync\_array\_size                                    | 1                                                            |
| innodb\_sync\_spin\_loops                                    | 30                                                           |
| innodb\_table\_locks                                         | ON                                                           |
| innodb\_temp\_data\_file\_path                               | ibtmp1:12M:autoextend                                        |
| innodb\_thread\_concurrency                                  | 0                                                            |
| innodb\_thread\_sleep\_delay                                 | 10000                                                        |
| innodb\_tmpdir                                               |                                                              |
| innodb\_undo\_directory                                      | \./                                                          |
| innodb\_undo\_log\_truncate                                  | OFF                                                          |
| innodb\_undo\_logs                                           | 128                                                          |
| innodb\_undo\_tablespaces                                    | 0                                                            |
| innodb\_use\_native\_aio                                     | ON                                                           |
| innodb\_version                                              | 5\.7\.30                                                     |
| innodb\_write\_io\_threads                                   | 4                                                            |
| insert\_id                                                   | 0                                                            |
| interactive\_timeout                                         | 28800                                                        |
| internal\_tmp\_disk\_storage\_engine                         | InnoDB                                                       |
| join\_buffer\_size                                           | 262144                                                       |
| keep\_files\_on\_create                                      | OFF                                                          |
| key\_buffer\_size                                            | 8388608                                                      |
| key\_cache\_age\_threshold                                   | 300                                                          |
| key\_cache\_block\_size                                      | 1024                                                         |
| key\_cache\_division\_limit                                  | 100                                                          |
| keyring\_operations                                          | ON                                                           |
| large\_files\_support                                        | ON                                                           |
| large\_page\_size                                            | 0                                                            |
| large\_pages                                                 | OFF                                                          |
| last\_insert\_id                                             | 0                                                            |
| lc\_messages                                                 | en\_US                                                       |
| lc\_messages\_dir                                            | /usr/local/mysql/share/                                      |
| lc\_time\_names                                              | en\_US                                                       |
| license                                                      | GPL                                                          |
| local\_infile                                                | ON                                                           |
| lock\_wait\_timeout                                          | 31536000                                                     |
| locked\_in\_memory                                           | OFF                                                          |
| log\_bin                                                     | OFF                                                          |
| log\_bin\_basename                                           |                                                              |
| log\_bin\_index                                              |                                                              |
| log\_bin\_trust\_function\_creators                          | OFF                                                          |
| log\_bin\_use\_v1\_row\_events                               | OFF                                                          |
| log\_builtin\_as\_identified\_by\_password                   | OFF                                                          |
| log\_error                                                   | /usr/local/mysql/log/mariadb\.log                            |
| log\_error\_verbosity                                        | 3                                                            |
| log\_output                                                  | FILE                                                         |
| log\_queries\_not\_using\_indexes                            | OFF                                                          |
| log\_slave\_updates                                          | OFF                                                          |
| log\_slow\_admin\_statements                                 | OFF                                                          |
| log\_slow\_slave\_statements                                 | OFF                                                          |
| log\_statements\_unsafe\_for\_binlog                         | ON                                                           |
| log\_syslog                                                  | OFF                                                          |
| log\_syslog\_facility                                        | daemon                                                       |
| log\_syslog\_include\_pid                                    | ON                                                           |
| log\_syslog\_tag                                             |                                                              |
| log\_throttle\_queries\_not\_using\_indexes                  | 0                                                            |
| log\_timestamps                                              | UTC                                                          |
| log\_warnings                                                | 2                                                            |
| long\_query\_time                                            | 10\.000000                                                   |
| low\_priority\_updates                                       | OFF                                                          |
| lower\_case\_file\_system                                    | OFF                                                          |
| lower\_case\_table\_names                                    | 1                                                            |
| master\_info\_repository                                     | FILE                                                         |
| master\_verify\_checksum                                     | OFF                                                          |
| max\_allowed\_packet                                         | 4194304                                                      |
| max\_binlog\_cache\_size                                     | 18446744073709547520                                         |
| max\_binlog\_size                                            | 1073741824                                                   |
| max\_binlog\_stmt\_cache\_size                               | 18446744073709547520                                         |
| max\_connect\_errors                                         | 100                                                          |
| max\_connections                                             | 600                                                          |
| max\_delayed\_threads                                        | 20                                                           |
| max\_digest\_length                                          | 1024                                                         |
| max\_error\_count                                            | 64                                                           |
| max\_execution\_time                                         | 0                                                            |
| max\_heap\_table\_size                                       | 16777216                                                     |
| max\_insert\_delayed\_threads                                | 20                                                           |
| max\_join\_size                                              | 18446744073709551615                                         |
| max\_length\_for\_sort\_data                                 | 1024                                                         |
| max\_points\_in\_geometry                                    | 65536                                                        |
| max\_prepared\_stmt\_count                                   | 16382                                                        |
| max\_relay\_log\_size                                        | 0                                                            |
| max\_seeks\_for\_key                                         | 18446744073709551615                                         |
| max\_sort\_length                                            | 1024                                                         |
| max\_sp\_recursion\_depth                                    | 0                                                            |
| max\_tmp\_tables                                             | 32                                                           |
| max\_user\_connections                                       | 0                                                            |
| max\_write\_lock\_count                                      | 18446744073709551615                                         |
| metadata\_locks\_cache\_size                                 | 1024                                                         |
| metadata\_locks\_hash\_instances                             | 8                                                            |
| min\_examined\_row\_limit                                    | 0                                                            |
| multi\_range\_count                                          | 256                                                          |
| myisam\_data\_pointer\_size                                  | 6                                                            |
| myisam\_max\_sort\_file\_size                                | 9223372036853727232                                          |
| myisam\_mmap\_size                                           | 18446744073709551615                                         |
| myisam\_recover\_options                                     | OFF                                                          |
| myisam\_repair\_threads                                      | 1                                                            |
| myisam\_sort\_buffer\_size                                   | 8388608                                                      |
| myisam\_stats\_method                                        | nulls\_unequal                                               |
| myisam\_use\_mmap                                            | OFF                                                          |
| mysql\_native\_password\_proxy\_users                        | OFF                                                          |
| net\_buffer\_length                                          | 16384                                                        |
| net\_read\_timeout                                           | 30                                                           |
| net\_retry\_count                                            | 10                                                           |
| net\_write\_timeout                                          | 60                                                           |
| new                                                          | OFF                                                          |
| ngram\_token\_size                                           | 2                                                            |
| offline\_mode                                                | OFF                                                          |
| old                                                          | OFF                                                          |
| old\_alter\_table                                            | OFF                                                          |
| old\_passwords                                               | 0                                                            |
| open\_files\_limit                                           | 65535                                                        |
| optimizer\_prune\_level                                      | 1                                                            |
| optimizer\_search\_depth                                     | 62                                                           |
| optimizer\_switch                                            | "index\_merge=on,index\_merge\_union=on,index\_merge\_sort\_union=on,index\_merge\_intersection=on,engine\_condition\_pushdown=on,index\_condition\_pushdown=on,mrr=on,mrr\_cost\_based=on,block\_nested\_loop=on,batched\_key\_access=off,materialization=on,semijoin=on,loosescan=on,firstmatch=on,duplicateweedout=on,subquery\_materialization\_cost\_based=on,use\_index\_extensions=on,condition\_fanout\_filter=on,derived\_merge=on" |
| optimizer\_trace                                             | "enabled=off,one\_line=off"                                  |
| optimizer\_trace\_features                                   | "greedy\_search=on,range\_optimizer=on,dynamic\_range=on,repeated\_subselect=on" |
| optimizer\_trace\_limit                                      | 1                                                            |
| optimizer\_trace\_max\_mem\_size                             | 16384                                                        |
| optimizer\_trace\_offset                                     | \-1                                                          |
| parser\_max\_mem\_size                                       | 18446744073709551615                                         |
| performance\_schema                                          | ON                                                           |
| performance\_schema\_accounts\_size                          | \-1                                                          |
| performance\_schema\_digests\_size                           | 10000                                                        |
| performance\_schema\_events\_stages\_history\_long\_size     | 10000                                                        |
| performance\_schema\_events\_stages\_history\_size           | 10                                                           |
| performance\_schema\_events\_statements\_history\_long\_size | 10000                                                        |
| performance\_schema\_events\_statements\_history\_size       | 10                                                           |
| performance\_schema\_events\_transactions\_history\_long\_size | 10000                                                        |
| performance\_schema\_events\_transactions\_history\_size     | 10                                                           |
| performance\_schema\_events\_waits\_history\_long\_size      | 10000                                                        |
| performance\_schema\_events\_waits\_history\_size            | 10                                                           |
| performance\_schema\_hosts\_size                             | \-1                                                          |
| performance\_schema\_max\_cond\_classes                      | 80                                                           |
| performance\_schema\_max\_cond\_instances                    | \-1                                                          |
| performance\_schema\_max\_digest\_length                     | 1024                                                         |
| performance\_schema\_max\_file\_classes                      | 80                                                           |
| performance\_schema\_max\_file\_handles                      | 32768                                                        |
| performance\_schema\_max\_file\_instances                    | \-1                                                          |
| performance\_schema\_max\_index\_stat                        | \-1                                                          |
| performance\_schema\_max\_memory\_classes                    | 320                                                          |
| performance\_schema\_max\_metadata\_locks                    | \-1                                                          |
| performance\_schema\_max\_mutex\_classes                     | 210                                                          |
| performance\_schema\_max\_mutex\_instances                   | \-1                                                          |
| performance\_schema\_max\_prepared\_statements\_instances    | \-1                                                          |
| performance\_schema\_max\_program\_instances                 | \-1                                                          |
| performance\_schema\_max\_rwlock\_classes                    | 50                                                           |
| performance\_schema\_max\_rwlock\_instances                  | \-1                                                          |
| performance\_schema\_max\_socket\_classes                    | 10                                                           |
| performance\_schema\_max\_socket\_instances                  | \-1                                                          |
| performance\_schema\_max\_sql\_text\_length                  | 1024                                                         |
| performance\_schema\_max\_stage\_classes                     | 150                                                          |
| performance\_schema\_max\_statement\_classes                 | 193                                                          |
| performance\_schema\_max\_statement\_stack                   | 10                                                           |
| performance\_schema\_max\_table\_handles                     | \-1                                                          |
| performance\_schema\_max\_table\_instances                   | \-1                                                          |
| performance\_schema\_max\_table\_lock\_stat                  | \-1                                                          |
| performance\_schema\_max\_thread\_classes                    | 50                                                           |
| performance\_schema\_max\_thread\_instances                  | \-1                                                          |
| performance\_schema\_session\_connect\_attrs\_size           | 512                                                          |
| performance\_schema\_setup\_actors\_size                     | \-1                                                          |
| performance\_schema\_setup\_objects\_size                    | \-1                                                          |
| performance\_schema\_users\_size                             | \-1                                                          |
| pid\_file                                                    | /usr/local/mysql/data/office\-UNION\-Dev\-07\.pid            |
| plugin\_dir                                                  | /usr/local/mysql/lib/plugin/                                 |
| port                                                         | 3306                                                         |
| preload\_buffer\_size                                        | 32768                                                        |
| profiling                                                    | OFF                                                          |
| profiling\_history\_size                                     | 15                                                           |
| protocol\_version                                            | 10                                                           |
| proxy\_user                                                  |                                                              |
| pseudo\_slave\_mode                                          | OFF                                                          |
| pseudo\_thread\_id                                           | 6894206                                                      |
| query\_alloc\_block\_size                                    | 8192                                                         |
| query\_cache\_limit                                          | 1048576                                                      |
| query\_cache\_min\_res\_unit                                 | 4096                                                         |
| query\_cache\_size                                           | 1048576                                                      |
| query\_cache\_type                                           | OFF                                                          |
| query\_cache\_wlock\_invalidate                              | OFF                                                          |
| query\_prealloc\_size                                        | 8192                                                         |
| rand\_seed1                                                  | 0                                                            |
| rand\_seed2                                                  | 0                                                            |
| range\_alloc\_block\_size                                    | 4096                                                         |
| range\_optimizer\_max\_mem\_size                             | 8388608                                                      |
| rbr\_exec\_mode                                              | STRICT                                                       |
| read\_buffer\_size                                           | 131072                                                       |
| read\_only                                                   | OFF                                                          |
| read\_rnd\_buffer\_size                                      | 262144                                                       |
| relay\_log                                                   |                                                              |
| relay\_log\_basename                                         | /usr/local/mysql/data/office\-UNION\-Dev\-07\-relay\-bin     |
| relay\_log\_index                                            | /usr/local/mysql/data/office\-UNION\-Dev\-07\-relay\-bin\.index |
| relay\_log\_info\_file                                       | relay\-log\.info                                             |
| relay\_log\_info\_repository                                 | FILE                                                         |
| relay\_log\_purge                                            | ON                                                           |
| relay\_log\_recovery                                         | OFF                                                          |
| relay\_log\_space\_limit                                     | 0                                                            |
| report\_host                                                 |                                                              |
| report\_password                                             |                                                              |
| report\_port                                                 | 3306                                                         |
| report\_user                                                 |                                                              |
| require\_secure\_transport                                   | OFF                                                          |
| rpl\_stop\_slave\_timeout                                    | 31536000                                                     |
| secure\_auth                                                 | ON                                                           |
| secure\_file\_priv                                           | NULL                                                         |
| server\_id                                                   | 0                                                            |
| server\_id\_bits                                             | 32                                                           |
| server\_uuid                                                 | 434601d6\-bf58\-11ea\-885e\-005056949a85                     |
| session\_track\_gtids                                        | OFF                                                          |
| session\_track\_schema                                       | ON                                                           |
| session\_track\_state\_change                                | OFF                                                          |
| session\_track\_system\_variables                            | "time\_zone,autocommit,character\_set\_client,character\_set\_results,character\_set\_connection" |
| session\_track\_transaction\_info                            | OFF                                                          |
| sha256\_password\_auto\_generate\_rsa\_keys                  | ON                                                           |
| sha256\_password\_private\_key\_path                         | private\_key\.pem                                            |
| sha256\_password\_proxy\_users                               | OFF                                                          |
| sha256\_password\_public\_key\_path                          | public\_key\.pem                                             |
| show\_compatibility\_56                                      | OFF                                                          |
| show\_create\_table\_verbosity                               | OFF                                                          |
| show\_old\_temporals                                         | OFF                                                          |
| skip\_external\_locking                                      | ON                                                           |
| skip\_name\_resolve                                          | OFF                                                          |
| skip\_networking                                             | OFF                                                          |
| skip\_show\_database                                         | OFF                                                          |
| slave\_allow\_batching                                       | OFF                                                          |
| slave\_checkpoint\_group                                     | 512                                                          |
| slave\_checkpoint\_period                                    | 300                                                          |
| slave\_compressed\_protocol                                  | OFF                                                          |
| slave\_exec\_mode                                            | STRICT                                                       |
| slave\_load\_tmpdir                                          | /tmp                                                         |
| slave\_max\_allowed\_packet                                  | 1073741824                                                   |
| slave\_net\_timeout                                          | 60                                                           |
| slave\_parallel\_type                                        | DATABASE                                                     |
| slave\_parallel\_workers                                     | 0                                                            |
| slave\_pending\_jobs\_size\_max                              | 16777216                                                     |
| slave\_preserve\_commit\_order                               | OFF                                                          |
| slave\_rows\_search\_algorithms                              | "TABLE\_SCAN,INDEX\_SCAN"                                    |
| slave\_skip\_errors                                          | OFF                                                          |
| slave\_sql\_verify\_checksum                                 | ON                                                           |
| slave\_transaction\_retries                                  | 10                                                           |
| slave\_type\_conversions                                     |                                                              |
| slow\_launch\_time                                           | 2                                                            |
| slow\_query\_log                                             | OFF                                                          |
| slow\_query\_log\_file                                       | /usr/local/mysql/data/office\-UNION\-Dev\-07\-slow\.log      |
| socket                                                       | /usr/local/mysql/mysql\.sock                                 |
| sort\_buffer\_size                                           | 262144                                                       |
| sql\_auto\_is\_null                                          | OFF                                                          |
| sql\_big\_selects                                            | ON                                                           |
| sql\_buffer\_result                                          | OFF                                                          |
| sql\_log\_bin                                                | ON                                                           |
| sql\_log\_off                                                | OFF                                                          |
| sql\_mode                                                    | "STRICT\_TRANS\_TABLES,NO\_ENGINE\_SUBSTITUTION"             |
| sql\_notes                                                   | ON                                                           |
| sql\_quote\_show\_create                                     | ON                                                           |
| sql\_safe\_updates                                           | ON                                                           |
| sql\_select\_limit                                           | 18446744073709551615                                         |
| sql\_slave\_skip\_counter                                    | 0                                                            |
| sql\_warnings                                                | OFF                                                          |
| ssl\_ca                                                      | ca\.pem                                                      |
| ssl\_capath                                                  |                                                              |
| ssl\_cert                                                    | server\-cert\.pem                                            |
| ssl\_cipher                                                  |                                                              |
| ssl\_crl                                                     |                                                              |
| ssl\_crlpath                                                 |                                                              |
| ssl\_key                                                     | server\-key\.pem                                             |
| stored\_program\_cache                                       | 256                                                          |
| super\_read\_only                                            | OFF                                                          |
| sync\_binlog                                                 | 1                                                            |
| sync\_frm                                                    | ON                                                           |
| sync\_master\_info                                           | 10000                                                        |
| sync\_relay\_log                                             | 10000                                                        |
| sync\_relay\_log\_info                                       | 10000                                                        |
| system\_time\_zone                                           | CST                                                          |
| table\_definition\_cache                                     | 1400                                                         |
| table\_open\_cache                                           | 2000                                                         |
| table\_open\_cache\_instances                                | 16                                                           |
| thread\_cache\_size                                          | 14                                                           |
| thread\_handling                                             | one\-thread\-per\-connection                                 |
| thread\_stack                                                | 262144                                                       |
| time\_format                                                 | %H:%i:%s                                                     |
| time\_zone                                                   | SYSTEM                                                       |
| timestamp                                                    | 1604368993\.645445                                           |
| tls\_version                                                 | "TLSv1,TLSv1\.1,TLSv1\.2"                                    |
| tmp\_table\_size                                             | 16777216                                                     |
| tmpdir                                                       | /tmp                                                         |
| transaction\_alloc\_block\_size                              | 8192                                                         |
| transaction\_allow\_batching                                 | OFF                                                          |
| transaction\_isolation                                       | REPEATABLE\-READ                                             |
| transaction\_prealloc\_size                                  | 4096                                                         |
| transaction\_read\_only                                      | OFF                                                          |
| transaction\_write\_set\_extraction                          | OFF                                                          |
| tx\_isolation                                                | REPEATABLE\-READ                                             |
| tx\_read\_only                                               | OFF                                                          |
| unique\_checks                                               | ON                                                           |
| updatable\_views\_with\_limit                                | YES                                                          |
| version                                                      | 5\.7\.30                                                     |
| version\_comment                                             | "MySQL Community Server \(GPL\)"                             |
| version\_compile\_machine                                    | x86\_64                                                      |
| version\_compile\_os                                         | linux\-glibc2\.12                                            |
| wait\_timeout                                                | 28800                                                        |
| warning\_count                                               | 0                                                            |

#### autocommit

```java
show variables like 'autocommit'; autocommit是针对连接的，在一个连接中修改了参数，不会对其他连接产生影响。如果关闭了autocommit，则所有的sql语句都在一个事务中，直到执行了commit或rollback，该事务结束，同时开始了另外一个事务。DDL语句(create table/drop table/alter/table)、lock tables语句在事务中执行了这些命令，会马上强制执行commit提交事务。
```

### SQL_SAFE_UPDATES

```sql
14:24:26	UPDATE contract_second  s SET      project_id = (SELECT              project_id         FROM             ghxc_ica.contract c         WHERE             s.contract_id = c.id)	Error Code: 1175. You are using safe update mode and you tried to update a table without a WHERE that uses a KEY column.  To disable safe mode, toggle the option in Preferences -> SQL Editor and reconnect.	0.078 sec

-- SQL_SAFE_UPDATES = 1时，不带where和limit条件的update和delete操作语句是无法执行的，即使是有where和limit条件但不带key column的update和delete也不能执行
-- 安全模式关闭
set sql_safe_updates=0; 

-- 安全模式打开
set sql_safe_updates=1;      
```



```sql
EXPLAIN UPDATE contract_second  s
SET 
    project_id = (SELECT 
            project_id
        FROM
            ghxc_ica.contract c
        WHERE
            s.contract_id = c.id);
```

| id   | select\_type         | table | partitions | type    | possible\_keys | key     | key\_len | ref                        | rows | filtered | Extra |
| ---- | -------------------- | ----- | ---------- | ------- | -------------- | ------- | -------- | -------------------------- | ---- | -------- | ----- |
| 1    | UPDATE               | s     | NULL       | index   | NULL           | PRIMARY | 8        | NULL                       | 42   | 100\.00  | NULL  |
| 2    | "DEPENDENT SUBQUERY" | c     | NULL       | eq\_ref | PRIMARY        | PRIMARY | 8        | ghxc\_ica\.s\.contract\_id | 1    | 100\.00  | NULL  |

```SQL
EXPLAIN UPDATE contract_second s
        LEFT JOIN
    contract c ON s.contract_id = c.id 
SET 
    s.project_id = c.project_id;  
```

| id   | select\_type | table | partitions | type    | possible\_keys | key     | key\_len | ref                        | rows | filtered | Extra |
| ---- | ------------ | ----- | ---------- | ------- | -------------- | ------- | -------- | -------------------------- | ---- | -------- | ----- |
| 1    | UPDATE       | s     | NULL       | ALL     | NULL           | NULL    | NULL     | NULL                       | 42   | 100\.00  | NULL  |
| 1    | SIMPLE       | c     | NULL       | eq\_ref | PRIMARY        | PRIMARY | 8        | ghxc\_ica\.s\.contract\_id | 1    | 100\.00  | NULL  |

## 死锁问题

```mysql
遇到死锁问题，先不要着急kill id，要先找到原因，不然埋下了一个定时炸弹

-- 查询未提交的事务
select t.trx_mysql_thread_id from information_schema.innodb_trx t;
kill {trx_mysql_thread_id};

-- 查看trx_mysql_thread_id是否在sleep线程中，若有则证明休眠的线程事务一直没commit提交或rollback回滚
show processlist;

select concat('KILL ',id,';') from information_schema.processlist where user='admin';

-- 当前所运行的所有事务
SELECT * FROM information_schema.INNODB_TRX;

-- 当前所有的锁
SELECT * FROM information_schema.INNODB_LOCKs;

-- 锁等待的对应的关系
SELECT * FROM information_schema.INNODB_LOCK_waits;

```



```java
JD 100-500 < 150  删除政采节点
YJ 非中投标2步，前端勾上报的时候要带上前面 最终施工单位参数
异常原因：
      for (int i = 0; i < nodes.size() - 1; i++) {
            if (nodes.get(i).getNode().getCode() == node) {
                nextNode = nodes.get(i + 1);
                break;
            }
        }

        Project updateProject = new Project();
        updateProject.setId(projectId);
        // 存在空指针
        updateProject.setStatus(nextNode.getNode().getCode());
        updateProject.setUpdater(ContextUtil.getCurrentUser().getUserId());
        projectMapper.updateById(updateProject);

日志：
2020-10-31 17:16:41.344 [ERROR] [http-nio-9091-exec-8] [] org.union.ica.controller.handler.ControllerExceptionHandler: system error :{}
org.springframework.dao.CannotAcquireLockException: 
### Error updating database.  Cause: com.mysql.cj.jdbc.exceptions.MySQLTransactionRollbackException: Lock wait timeout exceeded; try restarting transaction
### The error may exist in org/union/ica/mapper/ProjectNodeMapper.java (best guess)
### The error may involve org.union.ica.mapper.ProjectNodeMapper.insert-Inline
### The error occurred while setting parameters
### SQL: INSERT INTO project_node  ( project_id, node_order, status, node_code, creator,  updater )  VALUES  ( ?, ?, ?, ?, ?,  ? )
### Cause: com.mysql.cj.jdbc.exceptions.MySQLTransactionRollbackException: Lock wait timeout exceeded; try restarting transaction
; Lock wait timeout exceeded; try restarting transaction; nested exception is com.mysql.cj.jdbc.exceptions.MySQLTransactionRollbackException: Lock wait timeout exceeded; try restarting transaction
	at org.springframework.jdbc.support.SQLErrorCodeSQLExceptionTranslator.doTranslate(SQLErrorCodeSQLExceptionTranslator.java:262)
	at org.springframework.jdbc.support.AbstractFallbackSQLExceptionTranslator.translate(AbstractFallbackSQLExceptionTranslator.java:72)
	at org.mybatis.spring.MyBatisExceptionTranslator.translateExceptionIfPossible(MyBatisExceptionTranslator.java:73)
	at org.mybatis.spring.SqlSessionTemplate$SqlSessionInterceptor.invoke(SqlSessionTemplate.java:446)
	at com.sun.proxy.$Proxy105.insert(Unknown Source)
	at org.mybatis.spring.SqlSessionTemplate.insert(SqlSessionTemplate.java:278)
	at com.baomidou.mybatisplus.core.override.MybatisMapperMethod.execute(MybatisMapperMethod.java:58)
	at com.baomidou.mybatisplus.core.override.MybatisMapperProxy.invoke(MybatisMapperProxy.java:62)
	at com.sun.proxy.$Proxy132.insert(Unknown Source)
	at sun.reflect.GeneratedMethodAccessor268.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
	at java.lang.reflect.Method.invoke(Unknown Source)
	at org.springframework.aop.support.AopUtils.invokeJoinpointUsingReflection(AopUtils.java:343)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.invokeJoinpoint(ReflectiveMethodInvocation.java:198)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:163)
	at org.springframework.aop.interceptor.ExposeInvocationInterceptor.invoke(ExposeInvocationInterceptor.java:93)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:212)
	at com.sun.proxy.$Proxy133.insert(Unknown Source)
	at org.union.ica.service.impl.ProjectServiceImpl.addProject(ProjectServiceImpl.java:156)
	at org.union.ica.service.impl.ProjectServiceImpl$$FastClassBySpringCGLIB$$d0a44681.invoke(<generated>)
	at org.springframework.cglib.proxy.MethodProxy.invoke(MethodProxy.java:218)
	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.invokeJoinpoint(CglibAopProxy.java:749)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:163)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:295)
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:98)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:688)
	at org.union.ica.service.impl.ProjectServiceImpl$$EnhancerBySpringCGLIB$$9895b795.addProject(<generated>)
	at org.union.ica.controller.ProjectController.addProject(ProjectController.java:65)
	at org.union.ica.controller.ProjectController$$FastClassBySpringCGLIB$$6a655d33.invoke(<generated>)
	at org.springframework.cglib.proxy.MethodProxy.invoke(MethodProxy.java:218)
	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.invokeJoinpoint(CglibAopProxy.java:749)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:163)
	at org.springframework.security.access.intercept.aopalliance.MethodSecurityInterceptor.invoke(MethodSecurityInterceptor.java:69)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:688)
	at org.union.ica.controller.ProjectController$$EnhancerBySpringCGLIB$$a765a509.addProject(<generated>)
	at sun.reflect.GeneratedMethodAccessor694.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
	at java.lang.reflect.Method.invoke(Unknown Source)
	at org.springframework.web.method.support.InvocableHandlerMethod.doInvoke(InvocableHandlerMethod.java:190)
	at org.springframework.web.method.support.InvocableHandlerMethod.invokeForRequest(InvocableHandlerMethod.java:138)
	at org.springframework.web.servlet.mvc.method.annotation.ServletInvocableHandlerMethod.invokeAndHandle(ServletInvocableHandlerMethod.java:104)
	at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.invokeHandlerMethod(RequestMappingHandlerAdapter.java:892)
	at org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter.handleInternal(RequestMappingHandlerAdapter.java:797)
	at org.springframework.web.servlet.mvc.method.AbstractHandlerMethodAdapter.handle(AbstractHandlerMethodAdapter.java:87)
	at org.springframework.web.servlet.DispatcherServlet.doDispatch(DispatcherServlet.java:1039)
	at org.springframework.web.servlet.DispatcherServlet.doService(DispatcherServlet.java:942)
	at org.springframework.web.servlet.FrameworkServlet.processRequest(FrameworkServlet.java:1005)
	at org.springframework.web.servlet.FrameworkServlet.doPost(FrameworkServlet.java:908)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:660)
	at org.springframework.web.servlet.FrameworkServlet.service(FrameworkServlet.java:882)
	at javax.servlet.http.HttpServlet.service(HttpServlet.java:741)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:231)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
	at org.apache.tomcat.websocket.server.WsFilter.doFilter(WsFilter.java:53)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:103)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
	at org.springframework.boot.actuate.web.trace.servlet.HttpTraceFilter.doFilterInternal(HttpTraceFilter.java:88)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:109)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:320)
	at org.springframework.security.web.access.intercept.FilterSecurityInterceptor.invoke(FilterSecurityInterceptor.java:127)
	at org.springframework.security.web.access.intercept.FilterSecurityInterceptor.doFilter(FilterSecurityInterceptor.java:91)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334)
	at org.springframework.security.web.access.ExceptionTranslationFilter.doFilter(ExceptionTranslationFilter.java:119)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334)
	at org.springframework.security.web.session.SessionManagementFilter.doFilter(SessionManagementFilter.java:137)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334)
	at org.springframework.security.web.authentication.AnonymousAuthenticationFilter.doFilter(AnonymousAuthenticationFilter.java:111)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334)
	at org.springframework.security.web.servletapi.SecurityContextHolderAwareRequestFilter.doFilter(SecurityContextHolderAwareRequestFilter.java:170)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334)
	at org.springframework.security.web.savedrequest.RequestCacheAwareFilter.doFilter(RequestCacheAwareFilter.java:63)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334)
	at org.union.jwt.config.JwtAuthenticationTokenFilter.doFilterInternal(JwtAuthenticationTokenFilter.java:59)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:109)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334)
	at org.springframework.security.web.authentication.logout.LogoutFilter.doFilter(LogoutFilter.java:116)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334)
	at org.springframework.security.web.header.HeaderWriterFilter.doFilterInternal(HeaderWriterFilter.java:74)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:109)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334)
	at org.springframework.security.web.context.SecurityContextPersistenceFilter.doFilter(SecurityContextPersistenceFilter.java:105)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334)
	at org.springframework.security.web.context.request.async.WebAsyncManagerIntegrationFilter.doFilterInternal(WebAsyncManagerIntegrationFilter.java:56)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:109)
	at org.springframework.security.web.FilterChainProxy$VirtualFilterChain.doFilter(FilterChainProxy.java:334)
	at org.springframework.security.web.FilterChainProxy.doFilterInternal(FilterChainProxy.java:215)
	at org.springframework.security.web.FilterChainProxy.doFilter(FilterChainProxy.java:178)
	at org.springframework.web.filter.DelegatingFilterProxy.invokeDelegate(DelegatingFilterProxy.java:357)
	at org.springframework.web.filter.DelegatingFilterProxy.doFilter(DelegatingFilterProxy.java:270)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
	at org.springframework.web.filter.RequestContextFilter.doFilterInternal(RequestContextFilter.java:99)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:109)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
	at org.springframework.web.filter.FormContentFilter.doFilterInternal(FormContentFilter.java:92)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:109)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
	at org.springframework.web.filter.HiddenHttpMethodFilter.doFilterInternal(HiddenHttpMethodFilter.java:93)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:109)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
	at org.springframework.boot.actuate.metrics.web.servlet.WebMvcMetricsFilter.filterAndRecordMetrics(WebMvcMetricsFilter.java:114)
	at org.springframework.boot.actuate.metrics.web.servlet.WebMvcMetricsFilter.doFilterInternal(WebMvcMetricsFilter.java:104)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:109)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
	at org.springframework.web.filter.CharacterEncodingFilter.doFilterInternal(CharacterEncodingFilter.java:200)
	at org.springframework.web.filter.OncePerRequestFilter.doFilter(OncePerRequestFilter.java:109)
	at org.apache.catalina.core.ApplicationFilterChain.internalDoFilter(ApplicationFilterChain.java:193)
	at org.apache.catalina.core.ApplicationFilterChain.doFilter(ApplicationFilterChain.java:166)
	at org.apache.catalina.core.StandardWrapperValve.invoke(StandardWrapperValve.java:202)
	at org.apache.catalina.core.StandardContextValve.invoke(StandardContextValve.java:96)
	at org.apache.catalina.authenticator.AuthenticatorBase.invoke(AuthenticatorBase.java:490)
	at org.apache.catalina.core.StandardHostValve.invoke(StandardHostValve.java:139)
	at org.apache.catalina.valves.ErrorReportValve.invoke(ErrorReportValve.java:92)
	at org.apache.catalina.core.StandardEngineValve.invoke(StandardEngineValve.java:74)
	at org.apache.catalina.connector.CoyoteAdapter.service(CoyoteAdapter.java:343)
	at org.apache.coyote.http11.Http11Processor.service(Http11Processor.java:408)
	at org.apache.coyote.AbstractProcessorLight.process(AbstractProcessorLight.java:66)
	at org.apache.coyote.AbstractProtocol$ConnectionHandler.process(AbstractProtocol.java:853)
	at org.apache.tomcat.util.net.NioEndpoint$SocketProcessor.doRun(NioEndpoint.java:1587)
	at org.apache.tomcat.util.net.SocketProcessorBase.run(SocketProcessorBase.java:49)
	at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source)
	at org.apache.tomcat.util.threads.TaskThread$WrappingRunnable.run(TaskThread.java:61)
	at java.lang.Thread.run(Unknown Source)
Caused by: com.mysql.cj.jdbc.exceptions.MySQLTransactionRollbackException: Lock wait timeout exceeded; try restarting transaction
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:123)
	at com.mysql.cj.jdbc.exceptions.SQLError.createSQLException(SQLError.java:97)
	at com.mysql.cj.jdbc.exceptions.SQLExceptionsMapping.translateException(SQLExceptionsMapping.java:122)
	at com.mysql.cj.jdbc.ClientPreparedStatement.executeInternal(ClientPreparedStatement.java:955)
	at com.mysql.cj.jdbc.ClientPreparedStatement.execute(ClientPreparedStatement.java:372)
	at com.zaxxer.hikari.pool.ProxyPreparedStatement.execute(ProxyPreparedStatement.java:44)
	at com.zaxxer.hikari.pool.HikariProxyPreparedStatement.execute(HikariProxyPreparedStatement.java)
	at sun.reflect.GeneratedMethodAccessor121.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
	at java.lang.reflect.Method.invoke(Unknown Source)
	at org.apache.ibatis.logging.jdbc.PreparedStatementLogger.invoke(PreparedStatementLogger.java:59)
	at com.sun.proxy.$Proxy198.execute(Unknown Source)
	at org.apache.ibatis.executor.statement.PreparedStatementHandler.update(PreparedStatementHandler.java:47)
	at org.apache.ibatis.executor.statement.RoutingStatementHandler.update(RoutingStatementHandler.java:74)
	at sun.reflect.GeneratedMethodAccessor184.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
	at java.lang.reflect.Method.invoke(Unknown Source)
	at org.apache.ibatis.plugin.Plugin.invoke(Plugin.java:63)
	at com.sun.proxy.$Proxy197.update(Unknown Source)
	at com.baomidou.mybatisplus.core.executor.MybatisSimpleExecutor.doUpdate(MybatisSimpleExecutor.java:54)
	at org.apache.ibatis.executor.BaseExecutor.update(BaseExecutor.java:117)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.update(DefaultSqlSession.java:197)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.insert(DefaultSqlSession.java:184)
	at sun.reflect.GeneratedMethodAccessor269.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
	at java.lang.reflect.Method.invoke(Unknown Source)
	at org.mybatis.spring.SqlSessionTemplate$SqlSessionInterceptor.invoke(SqlSessionTemplate.java:433)
```



## 存储引擎

### MySQL5.7支持的存储引擎

```sql
-- '5.7.30'
select version();


show engines;
```

| Engine              | Support | Comment                                                      | Transactions | XA   | Savepoints |
| ------------------- | ------- | ------------------------------------------------------------ | ------------ | ---- | ---------- |
| InnoDB              | DEFAULT | "Supports transactions, row\-level locking, and foreign keys" | YES          | YES  | YES        |
| CSV                 | YES     | "CSV storage engine"                                         | NO           | NO   | NO         |
| MyISAM              | YES     | "MyISAM storage engine"                                      | NO           | NO   | NO         |
| BLACKHOLE           | YES     | "/dev/null storage engine \(anything you write to it disappears\)" | NO           | NO   | NO         |
| PERFORMANCE\_SCHEMA | YES     | "Performance Schema"                                         | NO           | NO   | NO         |
| MRG\_MYISAM         | YES     | "Collection of identical MyISAM tables"                      | NO           | NO   | NO         |
| ARCHIVE             | YES     | "Archive storage engine"                                     | NO           | NO   | NO         |
| MEMORY              | YES     | "Hash based, stored in memory, useful for temporary tables"  | NO           | NO   | NO         |
| FEDERATED           | NO      | "Federated MySQL storage engine"                             | NULL         | NULL | NULL       |

local数据库要访问远程数据库表中的数据，必须通过FEDERATED实现，类似Oracle中数据库链接(DBLINK)，使用FEDERATED修改安装目录C:\Program Files\MySQL\MySQL Server 5.7里的my-default.ini文件（先复制一份，再改），重启MySQL服务

在源数据库建个和目标数据库表（或视图）结构一样的表

```sql
Ex.CREATE TABLE federated_table (
    id     int(20) NOT NULL auto_increment,
    name   varchar(32) NOT NULL default '',
    other  int(20) NOT NULL default '0',
    PRIMARY KEY  (id),
    KEY name (name),
    KEY other_key (other)
) ENGINE=FEDERATED CONNECTION='mysql://username:password@remote_host:3306/db_name/table_name';

在源数据库执行select * from federated_table ，取出来的就是远程数据库的数据

```



## 事务

### 原理



### 事务管理器TransactionManager

跨库MySQL、Mongo的事务管理器只有一个执行后，切换另一个事务管理器不会再提交事务



### MySQL事务隔离级别

Serializable 串行化：避免脏读、不可重复读、幻读

RR Repeatable Read （MySQL默认）可重复读：避免脏读、不可重复读 

MySQL如何解决幻读？（1）MVVC 快照读、一致性读（2）next-key（当前读）锁包含记录锁（加在索引列的锁）、间隙锁（加在索引列之间的锁）

MySQL innoDB RR 通过快照读、当前读两种模式解决幻读问题

next-key原理是将当前数据行与上一条数据和下一条数据之间的间隙锁定，保证此范围内读取数据是一致的。

Read committed（Oracle默认，Oracle仅支持Serializable、Read committed） 读已提交：避免脏读

Read uncommitted 读未提交：最低级别，任何情况都无发提交

#### 脏、幻读（虚读）

脏读：事务A读取了一条记录的值，基于这条值做业务逻辑，在事务A提交之前，事务B回滚了该条记录，导致事务A读到了这条记录的一个脏数据。

脏读 T1读取了T2未提交数据

幻读（虚读）：一次事务里，多次查询后，结果集的个数不一致叫幻读。Ex.T1事务读123，T2事务插入4提交，T1再读库里1234。

MySQL可重复读的事务隔离级别前提下，T1事务读123，T2事务插入4，但T2提交后又撤销了，对T1事务的读并没有影响。

### 事务传播机制

什么是事务挂起？

如何内层的事务遇错不回滚？外层的事务不回滚？

### 事务回滚

执行SQL的connection与开启事务的connection必须是同一个才能对事务进行控制，事务Catch RuntimeException才回滚，常见的RuntimeException有？

往上抛的异常最上层才执行回滚

## 锁

where PK='XX' for update是一个行锁，for update是表锁，也是悲观锁，T1事务改表A并for update，T1不提交其他任何事务都改不了表A。数据库乐观锁还是CAS原理，常见实现是version、时间戳。

MySQL唯一索引和主键索引效率，主键（聚簇索引）优于唯一索引（非聚簇索引的一种是唯一索引，非聚簇索引包括复合索引）。

### GEN_CLUST_INDEX死锁

## 索引

### MySQL索引类型

| 索引类型 |      |
| :------: | :--- |
|  INDEX   |      |
|  UNIQUE  |      |
| PRIMARY  |      |
| SPATIAL  |      |
| FULLTEXT |      |

### MySQL索引失效

!=  <>不走索引

对索引列计算、函数、类型转换不走索引

is null、is not null不走索引

or 索引会失效

隐式转换（e.g. 字符串不加单引号）会索引失效

like '%XXX' 不走索引，为什么？数据大时前缀索引数据也会变得非常大，没有意义。但like reverse后走索引，也可以用覆盖索引，如下面的执行语句也不会全表扫描。

![Index ABC](http://hongchengjian.gitee.io/md/img/db/Index%20ABC.png)mysql in走索引吗？有时走有时不走

### MySQL复合索引ABC问题

索引是key index （a,b,c）。 支持a | a,b| a,b,c 3种组合进行查找，但不支持 b,c进行查找 .当最左侧字段是常量引用时，索引就十分有效。

(1) select * from myTest where a=3 and b=5 and c=4; ---- abc顺序
abc三个索引都在where条件里面用到了，而且都发挥了作用

(2) select * from myTest where c=4 and b=6 and a=3;
where里面的条件顺序在查询之前会被mysql自动优化，效果跟上一句一样

(3) select * from myTest where a=3 and c=7;
a用到索引，b没有用，所以c是没有用到索引效果的（b没有使用到，所以索引达不到 c ，所以c未使用索引）

(4) select * from myTest where a=3 and b>7 and c=3; ---- b范围值，断点，阻塞了c的索引
a用到了，b也用到了，c没有用到，这个地方b是范围值，也算断点，只不过自身用到了索引

(5) select * from myTest where b=3 and c=4; — 联合索引必须按照顺序使用，并且需要全部使用
a索引没有使用，所以这里 bc都没有用上索引效果

(6) select * from myTest where a>4 and b=7 and c=9;
a用到了 b没有使用，c没有使用（a用了范围所以，相当于断点，之后的b，c都没有用到索引）

(7) select * from myTest where a=3 order by b;
a用到了索引，b在结果排序中也用到了索引的效果，a下面任意一段的b是排好序的

(8) select * from myTest where a=3 order by c;
a用到了索引，但是这个地方c没有发挥排序效果，因为中间断点了，使用 explain 可以看到 filesort

(9) select * from mytable where b=3 order by a;
b没有用到索引，排序中a也没有发挥索引效果



### MySQL复合索引最左原则底层原理

B+Tree按照第一个key进行索引排列

![Complex Index](http://hongchengjian.gitee.io/md/img/db/Complex%20Index.png)

索引看distinct占比，index加在distinct rows区分度比较高的字段，占比不高的字段<30%不适合建立索引，不如全表扫快。不要为逻辑写复杂sql用聚合、计算函数放弃单列索引，因为对单列索引进行计算、聚合等函数操作会使索引失效，复合索引的字段一般不要超过3个，比如A、B、C字段区分度相差比较均匀，且都<30%不能明显区分表数据，如A占20%区分度，B占10%区分度，C占15%区分度，适合对 (A,C,B)建复合索引观察查询效率，注意distinct占比高要左倾。单列索引遇到null要避免条件查询传入的条件字段值也为null，不然大表就可能直接全表扫。组合索引（A,B,C）时，带头大哥A不能死，有A,AB,*ABC*三种组合。极端情况AC，A和C也会使用索引，前提是B要有序；普通情况下，A走索引，C不走索引。https://www.cnblogs.com/codeAB/p/6387148.html

索引列函数在查询索引列上发生函数调用（函数索引除外）。

or 两边条件都建立索引时才会使用索引，只要有一边不是就会全表扫描。or对结果集影响注意左右两边是否缺少（），Ex.  on  条件A and  (source =1 and type =2 or type = 3)   VS on  条件A and（（source =1 and type =2） or （type = 3））

## MySQL explain

explain、explain extended（showwarning 可查得优化后的查询语句、rows*filtered/100估算出当前表和比当前表id值小的表进行连接的行数）、explain partitions（若查询是基于分区表会显示将查询的分区）

MySQL执行计划关注| id | select_type | table | partitions | type |possible_keys | key  | key_len | ref  | rows | filtered | Extra 

```css
简单说明：
id是select查询列，是SQL执行顺利标识，从大到小执行，先执行语句编号大的，MySQL将select分为简单查询、复杂查询（3个分别是简单子查询、from子查询、union查询）。
select_type区分普通查询（simple）、联合查询、子查询等复杂查询。
简单子查询 Ex.select (select 1 from account) from account;
from子查询 Ex.select id from (select id from account) as A;
union查询 Ex.select 1 union all select 1;
```

MySQL explain index type从优到差：system（系统表、空表、一行数据）> const （where条件是PK、unique index查满足条件的一行记录）> eq_ref （关联时出现，驱动表只返回一行数据，这行数据且是关联表的PK或unique index且not null）> ref（一般条件等值查询，不限连接顺序，不限PK和Unique Index、普通索引）> fulltext(MySQL优先使用全文检索、不管代价) > ref_or_null > index_merge（查询走两个以上索引取交、并集，但or使用时要查所有索引，此时性能不优于range） >unique_subquery(where中in子查询) > index_subquery > range（in、between、>、<、>=、like） > index(索引全表扫、索引排序、索引分组) > ALL（全表扫、service层内存检索优化防OOM）

CAUTION：possible keys（罗列查询可能用到的所有索引）有列、key（查询真正使用到的索引，select type为index merge时，key可能多个）显示Null，表中数据不多，MySQL认为索引对查询帮助不大，直接全表扫

Q1: select 1 from XX 是 const 还是 system？

![mysql explain select 1 from dual](img/mysql explain select 1 from dual

.png)

![image-mysql explain select 1 from T](img/mysql explain select 1 from T.png)

Q2: 什么情况下建立索引后查询实际不走索引？

### Hive SQL VS SQL

Hive没有delete和update

### 分号符处理

select concat(key,concat(';',key)) from dual;分号符用ASCII

select concat(key,concat('\073',key)) from dual

## MySQL join

![join](http://hongchengjian.gitee.io/md/img/db/join.png)

inner join的连接中,mysql会自己评估使用a表查b表的效率高还是b表查a表高，如果两个表都建有索引的情况下，mysql同样会评估使用a表条件字段上的索引效率高还是b表

select * from tb1 a ,tb2 b where a.id=b.id  join笛卡尔积 执行方式是将表a和表b的记录组合起来，然后考察满足条件的，并返回。

select * from tb1 a inner join tb2 b on a.id=b.id  inner join 参照表a中的记录，一条一条到表b中去找符合记录的，符合则连在一起，否则转到a中下一条

# Hive

## Hive中文件存储格式及文件压缩方式

```css
1.文件存储方式: TextFile、SequenceFile、RCFile、ORCFile
2.TextFile: 默认格式，存储方式为行存储，数据不做压缩，磁盘开销大，数据解析开销大，可以结合GZIP和BZIP使用，压缩文件不支持Split，Hive不对数据进行切分，从而无法对数据进行并行操作。
3.SequenceFile: 由Hadoop API提供的一种二进制文件支持，具使用方便、可压缩，支持None、Record、Block三种压缩格式，Record压缩率低，一般使用Block。
4.RCFile: 按行分块，每块按列存储。RCFile不支持任意方式的数据写入，仅提供了一种追加接口。
5.ORCFile: 按行分块，每块按列存储，压缩快，快速列存取。 效率比RC
```

## Hive中三种自定义函数

```css
1.UDF:单行进入，单行输出。
2、UDAF:多行进入，单行输出。
3、UDTF:多行进入，多行输出。
```

## Hive的数据类型

### 简单数据类型

```css
1.整形
2.字符串类型
3.时间戳
4.浮点型
5.HIVE中的基础数据类型和JAVA一样
```

### 复杂数据类型

```css
1.数组
2.映射
3.结构体
```

### NULL类型

```
Hive底层是"\N"
```

## Hive四种表类型

```css
1.外部表
2.内部表
3.桶表
4.分区表
```

## Hive元数据三种保存方式

```css
1.内嵌式元存储服务器
2.本地元存储服务器
3.远程元存储服务器
```

## Hive数仓分层

```css
数据源：埋点采集、日志、Flume、Sqoop、Kettle等ETL工具导入HDFS，并映射到Hive数仓表中
ODS(原貌不做处理): Operation Data Store 原始数据层，存放原始数据，直接加载原始日志、数据保持原貌不做处理
DWD: Data Warehouse Detail 对ODS层数据进行清洗(去空、脏数据、超过极限范围数据、维度退化、降维、脱敏)
DWS: Data Warehouse Service 以DWD为基础，按天进行轻度汇总
DWT: Data Warehouse Topic 以DWS为基础，按主题进行汇总
ADS: Application Data Store 为各种统计报表提供数据
```

## HiveSQL转化成MR过程

```css
1.HiveSQL被Parser转化成AST
2.AST转化成Query Block
3.Query Block被转化成Operator Tree
4.优化Operator Tree
5.Operator Tree转化成MR任务
6.优化成最终的MR任务
```

## Hive与数据库交互

```

```



## Hive数据倾斜

### 原因

```css
1.key分布不均
2.数据本身问题
3.建表没考虑周全
4.SQL有数据倾斜
```

### 解决方案

```css
(1)给key一个随机的值，打散key
(2)Hive中参数调节①hive.map.aggr = true②hive.groupby.skewindata = true 作用：有数据倾斜时进行负载均衡，当选项设定位true，生成的查询计划会有两个MR Job。第一个MR Job中，Map的输出结果集合会随机分布到Reduce中，每个Reduce做部分聚合操作，并输出结果，这样处理的结果是相同的Group By Key有可能被分发到不同的Reduce中，从而达到负载均衡的目的；第二个MR Job再根据预处理的数据结果按照Group By Key 分布到 Reduce 中（这个过程可以保证相同的 Group By Key 被分布到同一个Reduce中），最后完成最终的聚合操作。
(3)SQL调节：1、选用join key分布最均匀的表作为驱动表。2、大小表join的时候，让维度较小的表先进内存。3、大表join的时候，把空值的key变成一个字符串加上一个随机数，把倾斜的数据分到不同的reduce上。4、count distinct大量相同特殊值
```

### Ex.SQL调节

COUNT(DISTINCT xxx)在 Hive中很容易造成数据倾斜

```sql
SELECT
  COUNT(DISTINCT uuid)
FROM detail_sdk_session t
WHERE t.date >= '2020-01-01' AND t.date <= now;

now表示当天的日期，越接近月末，上面的统计的数据量就会越大，只有一个reducer在进行COUNT(DISTINCT uuid)的计算，所有的数据都流向唯一的一个reducer，数据倾斜是必然的。
```

```sql
-- 外层SELECT求和
SELECT
  SUM(mau_part) mau
FROM
(
  -- 内层SELECT分别进行COUNT(DISTINCT)计算
  SELECT
    substr(uuid, 1, 3) uuid_part,
    COUNT(DISTINCT substr(uuid, 4)) AS mau_part
  FROM detail_sdk_session
  WHERE partition_date >= '2016-01-01' AND partition_date <= now
  GROUP BY substr(uuid, 1, 3)
) t;

内层SELECT根据uuid的前n位进行GROUP BY，并计算相应的活跃用户数COUNT(DISTINCT)，外层SELECT对COUNT(DISTINCT)结果进行求和，得到最终的月活跃用户数。 上面SQL中，n设为3，不应过大。原因：uuid是由字母和数字组成的：大写字母、小写字母和数字，字符总数为26+26+10=62，内层SELECT进行GROUP BY时，会有 62^n 个分组，外层SELECT就会进行 62^n 次求和。所以n不宜过大。当然，如果数据量十分巨大，n必须充分大，才能保证内层SELECT中的COUNT(DISTINCT)能够计算出来。
```

```sql
--  第三层SELECT
SELECT
  SUM(s.mau_part) mau
FROM
(
  -- 第二层SELECT
  SELECT
    tag,
    COUNT(*) mau_part
  FROM
  (
      -- 第一层SELECT
    SELECT
      uuid, 
      CAST(RAND() * 100 AS BIGINT) tag  -- 为去重后的uuid打上标记，标记为：0-100之间的整数。
    FROM detail_sdk_session
    WHERE partition_date >= '2016-01-01' AND partition_date <= now
    GROUP BY uuid   -- 通过GROUP BY，保证去重
   ) t
  GROUP BY tag
) s;

1.第一层SELECT：对uuid进行去重，并为去重后的uuid打上整数标记
2.第二层SELECT：按照标记进行分组，统计每个分组下uuid的个数
3.第三层SELECT：对所有分组进行求和 
上面这个方法最关键的是为每个uuid进行标记，这样就可以对其进行分组，分别计数，最后去和。如果数据量确实很大，也可以增加分组的个数。例如：CAST(RAND() * 1000 AS BIGINT) tag 
```

## Sort By VS Order By VS Cluster By VS Distribute By

```css
(1)sort by: 非全局排序，在数据进入reducer前完成排序
(2)order by: 会对输入做全局排序，因此只有一个reducer，如果有多个reducer无法保证全局的排序。计算规模较大，时间可能会很长。
(3)cluster by: 除了具有distribute by的功能，还具有了sort by的功能。
(4)distribute by：按照指定的字段对数据进行划分输出到不同的reduce中。
```

## Hive优化

```css
1.fetch抓取:修改配置文件hive.fetch.task.conversion为more，修改好全局查找和字段查找以及limit都不会触发MR任务。
2.本地模式:大多数的Hadoop Job要求Hadoop提供完整的可扩展性来触发大数据集，不过有时候Hive的输入数据量非常的小，这样的情况下可能触发任务的事件比执行的事件还长，可以通过本地模式把小量的数据放到本地上面计算
3.Group By:默认情况下，map阶段同一key的数据会发给一个reduce，当一个key数据过大就会倾斜，并不是所有的聚合操作都需要reduce端完成，很多聚合操作都可以现在map端进行部分聚合，最后在reduce端得出最终结果。(1)开启在map端聚合：hive.map.aggr = true。(2)在map端进行聚合操作的条目数：hive.groupby.mapaggr.checkinterval = 100000。(3)有数据倾斜的时候进行负载均衡：hive.groupby.skewindata = true。
4.count dinstinc去重：大的数据集先用count distinct查找重复的字段，然后用group by再去重。
5.行列过滤：列处理：只拿自己需要的列，如果有，尽量使用分区过滤。行处理：在分区裁剪的时候，当使用外关联的时候，先完全关联再过滤。
6.动态分区调整：(1)开启动态分区：hive.exec.dynamic.partition=true。(2)设置为非严格模式：hive.exec.dynamic.partiton.mode = nostrict。(3)实操：创建分区表、加载数据到分区表中、创建目标分区、设置动态分区、查看目标分区表的分区情况
7.小文件进行合并：在map执行之前合并小文件，减少map的数量，设置 set hive.input.format = org.apache.hadoop.hive.ql.io.CombineHiveInputFormat
8.调整map的数量和reduce的数量
9.并行执行：在Hive中可能有很多个阶段，不一定是一个阶段，这些阶段并非相互依赖的。然后这些阶段可以并行完成，设置并行：set hive.exec.parallel = true
10.JVM重用，缺点是task槽会被占用，一直要等到任务完成才会释放
```

## HiveQL

```css
Hive没有delete和update

分号符处理
select concat(key,concat(';',key)) from dual;分号符用ASCII
select concat(key,concat('\073',key)) from dual
```



#

# HBase

## 中间件持久化功能

```css
某一时刻机器挂了，还在内存但未处理完的数据不能凉
Redis有AOF和RDB、Elasticsearch会把数据写到translog然后结合FileSystemCache将数据刷到磁盘中、Kafka本身就是将数据顺序写到磁盘

先写Kafka暂存，后写Hive，Kafka数据不会单独取出来，持久化了的数据最常见用法是重新设置offset做回溯
Elasticsearch分布式搜索引擎，用于检索，没有经常检索的需求，数据写入Elasticsearch要分词浪费资源
HDFS不支持随机修改，查询效率低、对小文件支持不好(NameNode中因为大量的小文件的元数据，占用大量的内存空间)
```



```css
HBase也面向列，依赖Hadoop，适合统计维度不确定，可在廉价PC上搭建大规模结构化存储群。
(1)对象存储(适合图片、网页、新闻、病毒库)；
(2)时空数据(轨迹、气象、滴滴打车轨迹、车联网数据)；
(3)时序数据(分布在时间上的一系列数值，HBase OpenTSDB，设备、传感器采样、多维查询、时间段内数据查询)；
(4)推荐画像(Ex.蚂蚁风控，用户画像是一个比较大的稀疏矩阵，数据量巨大，用户标签多，统计维度不确定)；
(5)消息/订单(电信、银行、通信、通话、物流、浏览、交易、消费等消息构建在HBase之上)；
(6)Feed流(RSS中用来接收信息源更新的接口，持续更新并呈现给用户的内容，Ex.App收到的新文章推送，微博关注更新的类容)；
(7)NewSQL(HBase上Phoenix插件，满足二级索引、需要SQL非事务的需求)；

HBase不是OLTP，作为NoSQL，顶多是OLP，没有transaction，仅在rowkey上支持索引。性能不如Memcahed和Redis，持久化存储比NoSQL内存强。HBase也

```



## HBase Salting

```css
HBase存数据，若不加任何处理，数据会集中在几个Region，导致(1)写性能不断下降，(2)用MR处理时，个别map处理非常耗时
HBase中，表数据按Region存储，每个Region有Startkey，EndKey，默认情况下新建表只有一个Region，随不断写入数据，数据越来越多，Region的size越来越大超过阀值时，Region会split成两个Region，依次不断增加。缺陷是写性能不断下降，数据集中在几个Region，Region经常Split会导致RegionServer停顿造成性能问题
```



# Redis

## Redis VS Tair VS MemCache

MemCache单个value限制1M，不支持主从、不支持分片，适合玩单机本地。

Redis存较大value（最大512M）、较大key的数据(阻塞后有雪崩风险)。Redis是位存储内存贵，从成本上考虑不利于作为海量数据高性能读写。Redis单行命令读写具原子性、多行不具原子性，Redis无事务，若要保证事务，需通过Lua插件。Redis单机CP，单进程多线程。Redis集群是AP。

Tair是2010年淘宝研发的Key/Value数据存储系统，四种引擎mdb(基于MemCache)、rdb(基于Redis)、kdb(基于Kyoto Cabinet)、lob(基于Leveldb)。

Redis没有提供sharding封装，但Tair提供给了sharding封装。Tair对每个数据都包含版本号，版本号在每次更新后都递增，解决并发操作同一条数据的问题，如key的value为'a,b,c'，操作A加一个d，value为'a,b,c,d'，操作B加一个e，value为'a,b,c,e'，不加版本控制，操作A和B谁先更新会覆盖后面的更新值。非持久化（mdb,rdb），持久化（kdb,ldb）。

热数据(访问频繁)、缓压力(下游DB)、预热(长驻内存数据) 

使用缓存最重要确保抽离整个缓存，系统还能运转。

## Epoll指令

```css
epoll_create  创建一个epoll FD File Discriptor。
epoll_ctl 用来添加/修改/删除需要侦听的文件描述符及其事件。
epoll_wait 接收发生在被侦听的描述符上的，用户感兴趣的IO事件(短链接中大量调用造成系统瓶颈)。
```

## FD

```css
File Descriptor 文件描述符。
每一个文件描述符会与一个打开文件相对应。
不同的文件描述符也会指向同一个文件。
相同的文件可以被不同的进程打开也可以在同一个进程中被多次打开。
```

## Epoll VS Select/Poll

1G内存 Epoll可打开的FD是10W左右，而Select是默认FD_SETSIZE 1024。

Select/Poll有很大socket集合时，每次调用会线性扫描全部的集合导致IO效率线性下降，Epoll只会对活跃socket进行操作。

高速的LAN，Epoll效率并不一定比Select/Poll高，一旦使用idle connection模拟WAN环境，Epoll效率远在Select/poll之上。

## 集群模式

### (1)主从

架构一主多从，主存在单点风险，主从同步是全量复制耗内存，难在线扩容，从库进行replication可避免单点故障，主库Master可读也可写，写库自动同步给从库Slave，Slave只读不写。

主从复制策略： 一主多从(主写入压力大、主挂了，从库选举期间阻塞问题)、树状主从(利于CRC16算法将Slot均匀分配到不同主节点)

#### 主从复制细节原理

全量同步 VS 增量同步

##### 全量同步

```css
Redis全收到量复制在Slave初始化阶段，Slave需将Master所有数据都复制一份
(1)Slave连接Master，发送SYNC
(2)Master接受到SYNC后，执行BGSAVE生成RDB并记录缓冲区记录此后执行的所有写命令
(3)Master BGSAVE执行完后，向所有服务器发送快照文件，并在发送期间继续记录被执行的写命令
(4)Slave收到快照文件后丢弃所有旧数据，载入收到的快照
(5)Master发送快照完成后，开始向Slave发送缓冲区中的写命令
(6)Slave完成对快照载入，开始接受命令请求，并执行来自主服务器缓冲区的写命令
```

##### 增量同步

```css
Redis增量同步在Slave初始化开始正常工作时主服务器发生的写操作同步到从服务器的过程
增量复制的过程是Master每执行一个写命令就会向Slave发生相同的写命令，Slave接收并执行收到的写命令
```

##### 主从同步策略

```css
主从刚连接，进行全量同步，全量同步结束后，进行增量同步。若有需要，Slave在任何时候都可发起全量同步。Redis策略是无论如何首先尝试进行增量同步，若不成功，要求Slave进行全量同步。
```

##### 主从同步注意点

```css
(1)Redis使用异步复制，一个Master可以有多个Slave，多个Slave也可连接到一个Slave上
(2)主从同步不阻塞Master(当若干个Slave进行同步时，Master仍然可以处理请求)
```

### (2)哨兵

```css
故障切换(failover)哨兵负责主库宕机之后的投票选举，实现自动化故障发现和转移。
监控(1)主库和从库是否正常运行。(2)主库挂了，从库是否能切过去成为新主库(Pub、Sub)
tmpwatch --atime 30d /tmp 清除/tmp目录下30天没有被访问文件
```

Sentinel心跳+投票裁决 自动监控Master/Slave

补充 sentine config

```shell
tmpwatch --atime 30d /tmp 清除/tmp目录下30天没有被访问文件
```

### (3)代理

### (4)Redis Cluster 去中心化分片集群

Redis Cluster是Redis 3.0+之后官方推荐，基于HASH_SLOT = CRC16(key) mod 16384实现集群分片和数据跨主机转移和共享，可以实现Redis动态扩容和缩容。注意HASH_SLOT只会分配给主库，从库不会被分配。HASH_SLOT目的是分摊key到片区的主库，减少雪崩风险，缓解传统单一主库的压力。如果写入的key计算出的HASH_SLOT不在当前操作的主库 HASH_SLOT_RANGE内，会自动将key转发到HASH_SLOT_RANGE包含HASH_SLOT的主库进行写。

3.0+支持sharding，无中心网状结构，使用端连接任何一个节点即可，节点动态添加、动态删除不影响集群，端与Redis节点连接不需走Proxy层。半数节点检测到某个节点失效则判定节点失效。在resharding期间，原来同一个HASH_SLOT的key被迁移到不同的node中，multi-key操作可能不可用。

#### Redis Cluster VS 传统Redis集群

```css
传统集群缺陷：(1)始终只有一个主库接收和处理写，主库和从库完全同步，同步效率低，大量冗余数据(2)读写分离只有主库写，高并发下主库压力大，主同步从负荷加重，若过程中出现雪崩导致大量key失效和丢失数据(3)中心化集群方案：任何时候都需保证至少一个主库正常运行，主库宕机后，哨兵模式正在投票选举，由于在投票选举之前，谁也不知道新主库是谁，Redis会开启保护机制、禁止写操作直到选举出新主库)，主库和从库耦合度高。
```

#### 搭建

```
https://blog.csdn.net/qq_30056341/article/details/103320138 补充画出机器模型，尝试搭建
```

## 持久化AOF和RDB

Redis两种持久化，一种RDB直接从内存dump到磁盘，fork一个子进程先将数据写临时文件(副本：内存中的数据是原来2倍），写成功则将临时文件替换掉原文件，再二进制压缩。在指定的时间间隔内，执行指定次数的写操作，则会将内存中的数据写入到磁盘中。即在指定目录下生成一个dump.rdb文件。Redis 重启会通过加载dump.rdb文件恢复数据。

```css
# save ""
save 900 1
save 300 10
save 60 10000

#指定本地数据库文件名，一般采用默认的 dump.rdb
dbfilename dump.rdb

#指定本地数据库存放目录，一般也用默认配置
dir ./

#默认开启数据压缩，LZF压缩方式
rdbcompression yes
```

另一种AOF，以日志文本记录每一个写、删除操作，查询不记录，追加写入文件，Append of File。

## 常用Jar

```spreadsheet
redisTemplate、jedis、redisson
jar包常用jedis-2.9.0.jar、spring-data-commons-1.8.4.RELEASE.jar、spring-data-redis-1.8.4.RELEASE.jar
```

## 数据结构和命令

http://redisdoc.com/ 

eval(执行Lua)、scan(cursor based iterator)、HSCAN、ZSCAN

注意思考命令算法复杂度、空间复杂度，时间复杂度是O(n)涉及命令还有哪些？

思考批量操作命令有哪些？

```css
String: MSET、MSETNX、MGET
List: LPUSH、RPUSH、LRANGE、LINDEX、LSET、LINSERT
Hash: HDEL、HGETALL、HKEYS/HVALS
Set: SADD、SREM、SRANDMEMBER、SPOP、
		谨慎使用 SMEMBERS、SUNION/SUNIONSTORE、SINTER/SINTERSTORE、SDIFF/SDIFFSTO
Sorted Set: ZADD、ZREM、
		谨慎使用 O(Log(N)+M):ZRANGE/ZREVRANGE、ZRANGEBYSCORE/ZREVRANGEBYSCORE、ZREMRANGEBYRANK/ZREMRANGEBYSCORE
DEL、KEYS(会占用唯一线程的大量处理时间，导致所有请求都被拖慢)
```

为什么在删除hash set list等复杂元素时 时间复杂度不为O(1) 不能一次性删除hash等里面的所有元素吗，为什么要遍历删除?
DEL的时间复杂度是O(1)还是O(n)？
时间复杂度为O(1)命令有哪些？

### String

```css
JSONString、ToString、StringFormat等任何形式的String

SET 若key已经持有其他值， SET就覆写旧值，无视类型
SETNX SET if Not Exists若不存在，则 SET。若key 已经存在，则 SETNX 不做任何动作。
SETEX 将value 关联到 key，并将 key 的生存时间设为 seconds, key 已经存在， SETEX 命令将覆写旧值。
PSETEX 将value 关联到 key，并将 key 的生存时间设为毫秒
GET
GETSET  将给定 key 的值设为 value ，并返回 key 的旧值(old value)。当 key 存在但不是字符串类型时，返回一个错误。当key没有旧值，key不存在时，返回nil
STRLEN
APPEND
SETRANGE
GETRANGE
INCR 使用场景：热点+时效(1)热点数据：交易行为、库存、商品浏览数、问题、帖子、回复数、点赞数(2)时效信息存储，巧妙利用过期时间：App登陆码30s有效、session防止一个用户多长时间内重复登录、验证码(短信、图形、邮件)
某个用户一分钟内只能发三条短信验证码验证，set key exprireTime =60s，每发一次短信就incre key + 1，limit 3条可放Apollo配置中心，每次发短信前判断get key value <= limit。
INCRBY 
INCRBYFLOAT
DECR
DECRBY
MSET
MSET key1 value1 key2 value2 .. keyN valueN
MSET 涉及相关Redis源码：void msetGenericCommand(redisClient *c, int nx) / t_string.c
 
每分钟某个用户访问服务接口数不超过阀值n次，set key exprireTime = 60s，每访问一次就incre key + 1。  
MSET是原子命令Atomic，PIPELINE是非原子命令，Atomic：一个不可分割的最小工作单位，都成功或都失败。

无论Redis Cluster 还是Codis，批量操作MGET、MSET命令都受限；事务受限。
PIPELINE效率比MSET批量效率高些，Redis执行1次操作时间 = 1次网络时间 + 1次命令时间，执行n 次操作时间 = n 次网络时间 + n 次命令时间。执行1次PIPELINE(n条命令) = 1次网络时间 + n次命令时间，注意PIPELINE一次携带的数据量过大会影响1次网络时间过长。Redis在真正处理批量数据时是单线程For，执行到For时会独占CPU，但比耗在TCP闭合有价值。注意Redis Cluster是不支持PIPELINE和MSET命令，PIPELINE每次只能作用在一个Redis节点上。

PIPELINE是 http://redisdoc.com/中没有的，PIPELINE是Jedis包中提供，原理是一组命令放在MULTI和EXEC之间，注意DISCARD可以停止，但已执行的命令不能回滚。严格说：Redis不支持事务。MULTI和EXEC之间命令错误，语法不正确，导致事务不能正常结束，直接抛error：EXECABORT Transaction discarded because of previous error；运行错误，语法正确，但类型错误，事务可以正常结束，最后一步是OK，中间会报error；使用WATCH后，MULTI失效。

MSETNX
MGET
```

#### Jedis PIPELINE(微盟面试题)

```java
@Configuration
public class JedisClusterConfig {

    @Value("${spring.redis.cluster.nodes}")
    private String clusterNodes;

    @Value("${spring.redis.cache.commandTimeout}")
    private Integer commandTimeout;

    @Bean
    public JedisCluster getJedisCluster() {

        String[] serverArray = clusterNodes.split(",");
        Set<HostAndPort> nodes = new HashSet<>();
        for (String ipPort : serverArray) {
            String[] ipPortPair = ipPort.split(":");
            nodes.add(new HostAndPort(ipPortPair[0].trim(), Integer.valueOf(ipPortPair[1].trim())));
        }
        return new JedisCluster(nodes, commandTimeout);
    }
}

@Component
public class JedisClusterUtil {

    @Autowired
    private JedisCluster jedisCluster;

    @Resource(name = "redisTemplate4Json")
    protected RedisTemplate<String, Object> redisTemplate;

    /**
     * ZSet批量查询
     * @param keys
     * @return
     */
    public List<Object> batchZRange(List<String> keys) {

        List<Object> resList = new ArrayList<>();
        if (keys == null || keys.size() == 0) {
            return resList;
        }

        if (keys.size() == 1) {
            BoundZSetOperations<String, Object> operations = redisTemplate.boundZSetOps(keys.get(0));
            Set<Object> set = operations.reverseRange(0, 0);
            resList.add(set.iterator().next());
            return resList;
        }

        Map<JedisPool, List<String>> jedisPoolMap = getJedisPool(keys);

        List<String> keyList;
        JedisPool currentJedisPool = null;
        Pipeline currentPipeline;
        List<Object> res = new ArrayList<>();
        Map<String, Object> resultMap = new HashMap<>();

        //执行
        for (Map.Entry<JedisPool, List<String>> entry : jedisPoolMap.entrySet()) {
            Jedis jedis = null;
            try {
                currentJedisPool = entry.getKey();
                keyList = entry.getValue();
                //获取pipeline
                jedis = currentJedisPool.getResource();
                currentPipeline = jedis.pipelined();
                for (String key : keyList) {
                    currentPipeline.zrevrange(key, 0, 0);
                }
                //从pipeline中获取结果
                res = currentPipeline.syncAndReturnAll();
                currentPipeline.close();
                for (int i = 0; i < keyList.size(); i++) {
                    if (null == res.get(i)) {
                        resultMap.put(keyList.get(i), null);
                    } else {
                        Set<Object> set = (Set<Object>) res.get(i);
                        if (null == set || set.isEmpty()) {
                            resultMap.put(keyList.get(i), null);
                        } else {
                            byte[] byteStr = set.iterator().next().toString().getBytes();
                            Object obj = redisTemplate.getDefaultSerializer().deserialize(byteStr);
                            resultMap.put(keyList.get(i), obj);
                        }
                    }
                }
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                returnResource(jedis, currentJedisPool);
            }
        }
        resList = sortList(keys, resultMap);
        return resList;
    }

    /**
     * Value批量查询
     * @param keys
     * @return
     */
    public List<Object> batchGet(List<String> keys){
        List<Object> resList = new ArrayList<>();
        if (keys == null || keys.size() == 0) {
            return resList;
        }

        if (keys.size() == 1) {
            BoundValueOperations<String, Object> operations = redisTemplate.boundValueOps(keys.get(0));
            resList.add(operations.get());
            return resList;
        }

        Map<JedisPool, List<String>> jedisPoolMap = getJedisPool(keys);

        List<String> keyList;
        JedisPool currentJedisPool = null;
        Pipeline currentPipeline;
        List<Object> res = new ArrayList<>();
        Map<String, Object> resultMap = new HashMap<>();

        for (Map.Entry<JedisPool, List<String>> entry : jedisPoolMap.entrySet()) {
            Jedis jedis = null;
            try {
                currentJedisPool = entry.getKey();
                keyList = entry.getValue();
                //获取pipeline
                jedis = currentJedisPool.getResource();
                currentPipeline = jedis.pipelined();
                for (String key : keyList) {
                    currentPipeline.get(key);
                }
                //从pipeline中获取结果
                res = currentPipeline.syncAndReturnAll();
                currentPipeline.close();
                for (int i = 0; i < keyList.size(); i++) {
                    if (null == res.get(i)) {
                        resultMap.put(keyList.get(i), null);
                    } else {
                        byte[] byteStr = keyList.get(i).toString().getBytes();
                        Object obj = redisTemplate.getDefaultSerializer().deserialize(byteStr);
                        resultMap.put(keyList.get(i), obj);
                    }
                }
            } catch (Exception e) {
                e.printStackTrace();
            } finally {
                returnResource(jedis, currentJedisPool);
            }
        }
        resList = sortList(keys, resultMap);
        return resList;
    }

    private Map<JedisPool, List<String>> getJedisPool(List<String> keys){
        //JedisCluster继承了BinaryJedisCluster
        //BinaryJedisCluster的JedisClusterConnectionHandler属性
        //里面有JedisClusterInfoCache，根据这一条继承链，可以获取到JedisClusterInfoCache
        //从而获取slot和JedisPool直接的映射
        MetaObject metaObject = SystemMetaObject.forObject(jedisCluster);
        JedisClusterInfoCache cache = (JedisClusterInfoCache) metaObject.getValue("connectionHandler.cache");
        //保存地址+端口和命令的映射
        Map<JedisPool, List<String>> jedisPoolMap = new HashMap<>();

        JedisPool currentJedisPool = null;
        List<String> keyList;
        for (String key : keys) {
            //计算哈希槽
            int crc = JedisClusterCRC16.getSlot(key);
            //通过哈希槽获取节点的连接
            currentJedisPool = cache.getSlotPool(crc);

            //由于JedisPool作为value保存在JedisClusterInfoCache中的一个map对象中，每个节点的
            //JedisPool在map的初始化阶段就是确定的和唯一的，所以获取到的每个节点的JedisPool都是一样
            //的，可以作为map的key
            if (jedisPoolMap.containsKey(currentJedisPool)) {
                jedisPoolMap.get(currentJedisPool).add(key);
            } else {
                keyList = new ArrayList<>();
                keyList.add(key);
                jedisPoolMap.put(currentJedisPool, keyList);
            }
        }
        return jedisPoolMap;
    }

    private List<Object> sortList(List<String> keys, Map<String, Object> params) {
        List<Object> resultList = new ArrayList<>();
        Iterator<String> it = keys.iterator();
        while (it.hasNext()) {
            String key = it.next();
            resultList.add(params.get(key));
        }
        return resultList;
    }

    /**
     * 释放jedis资源
     *
     * @param jedis
     */
    public void returnResource(Jedis jedis, JedisPool jedisPool) {
        if (jedis != null && jedisPool != null) {
            jedisPool.returnResource(jedis);
        }
    }
```



### Hash

```css
大Key：小Key-Value键值对
涉及命令hset、hget、hmset、hmget、hkeys、hvals。使用场景(1)大业务对象、层级对象直接序列化 (2)结构化数据如JSON
Redis hash的底层是hashtable？
Redis存省，城市信息结构该如何设计？

HSET
HSETNX
HGET
HEXISTS
HDEL
HLEN
HSTRLEN
HINCRBY
HINCRBYFLOAT
HMSET
HMGET
HKEYS
HVALS
HGETALL
HSCAN
```

### List

```css
列表(有序，按插入顺序排序)涉及命令lpush、rpush、lrang、lindex、lset。使用场景：(1)消息队列，利用过期时间来做延时，好处是消费性能很高，最致命缺陷是缺少ACK，具体命令涉及BLPOP/BRPOP，参考https://redis.io/topics/data-types-intro中Blocking operations on lists，优先选型kafka(实时高吞吐量，丢数据，加ZooKeeper搭集群多份replica可减少丢数据的情况)、rabbitMQ(自定义延时，缺陷有序消费实现binding key、routing key复杂)、rocketMQ(仅支持18level延时缺陷，优点是积压能力是几个MQ中最好的，RocketMQ具备XA的事务能力)替代list(2)最新上架推荐产品 ltrim 可修剪出从start到stop指定范围的元素。
LPUSH list左侧插入1个或多个元素
LPUSHX
RPUSH
RPUSHX
LPOP
RPOP
RPOPLPUSH
LREM
LLEN
LINDEX
LINSERT
LSET
LRANGE
LTRIM
BLPOP
BRPOP
BRPOPLPUSH
```

### Set

```css
集合(各个元素都不同，但不是自动有序的)涉及命令 sadd、smembers、spop、sdiff、sunion。使用场景(1)去重，比如爬虫增量式爬取时对URI去重 (2)交并差集，比如用户行为的相似度分析，不同用户感兴趣的商品数量、社交共同好友的关注度分析
SADD
SISMEMBER
SPOP
SRANDMEMBER
SREM
SMOVE
SCARD
SMEMBERS
SSCAN
SINTER
SINTERSTORE
SUNION
SUNIONSTORE
SDIFF
SDIFFSTORE
```

### ZSet

```css
有序集合 
利用了一个Score参数来存储数据自动排序，为了优化排序和查找性能，items内容在大于64时同时使用了hash和skiplist，小于64时是ziplist（元素很小的情况下省内存），时间复杂度是O(n)涉及命令zadd、zrange、zcard。使用场景(1)有序不重复，比如商品热度，购买量作为score，Sorted Set按售卖量排序(2)自动排序需求
ZSet(有序)底层数据结构包括ziplist或skiplist。
ziplist vs skiplist
ziplist 使用内存更小 为什么内存小？ ziplist会比hashtable节省内存，节省大约50%。ziplist采用一段连续的内存来存储数据，相比hashtable减少了内存碎片和指针的内存占用。而且当节点较少时，ziplist更容易被加载到CPU缓存中。
skiplist的增加元素时间复杂度是、查询平均是O(n)？还是O(lgn)？
O(lgn)  推理论文参考 https://klevas.mif.vu.lt/~ragaisis/ADS2006/skiplists.pdf

ZADD
ZSCORE
ZINCRBY
ZCARD
ZCOUNT
ZRANGE
ZREVRANGE
ZRANGEBYSCORE
ZREVRANGEBYSCORE
ZRANK
ZREVRANK
ZREM
ZREMRANGEBYRANK
ZREMRANGEBYSCORE
ZRANGEBYLEX
ZLEXCOUNT
ZREMRANGEBYLEX
ZSCAN
ZUNIONSTORE
ZINTERSTORE
HyperLogLog
PFADD
PFCOUNT
PFMERGE
```

有关ziplist配置 config get *ziplist*
1) “hash-max-ziplist-entries”
2) “512”
3) “hash-max-ziplist-value”
4) “64”
5) “list-max-ziplist-entries”
6) “512”
7) “list-max-ziplist-value”
8) “64”
9) “zset-max-ziplist-entries”
10) “128”
11) “zset-max-ziplist-value”
12) “64”
-entries表示ziplsit对多保存数据项的个数，超出之后不能再使用ziplist
-value表示每个数据项的最大字节数，超出之后不能再使用ziplis

### 其他

```css
地理位置
GEOADD
GEOPOS
GEODIST
GEORADIUS
GEORADIUSBYMEMBER
GEOHASH

位图
SETBIT
GETBIT
BITCOUNT
BITPOS
BITOP
BITFIELD

数据库
EXISTS
TYPE
RENAME
RENAMENX
MOVE
DEL
RANDOMKEY
DBSIZE
KEYS
SCAN
SORT
FLUSHDB
FLUSHALL
SELECT
SWAPDB

自动过期
EXPIRE	set key value expireTime(Long)再set key value2，expireTime时间到，get key 有值吗？Redis过期时间原理？
1消极：每次访问key时判断key是否已经过期；
2积极；周期性的从设置了过期时间的key中选择一部分的key进行删除
a、随机测试20个带有timeout信息的key
b、如果超过25%的key被删除，则重复执行整个流程
Specifically this is what Redis does 10 times per second:
1.Test 20 random keys from the set of keys with an associated expire.
2.Delete all the keys found expired.
3.If more than 25% of keys were expired, start again from step 1.

Redis Hash结构小键值对能单独设置不同的过期时间吗？不能，Redis EXPIRE只对顶级key有效
EXPIREAT
TTL


PERSIST
PEXPIRE
PEXPIREAT
PTTL

事务
MULTI
EXEC
DISCARD
WATCH
UNWATCH

Lua 脚本
EVAL
EVALSHA
SCRIPT_LOAD
SCRIPT_EXISTS
SCRIPT_FLUSH
SCRIPT_KILL

持久化
SAVE
BGSAVE
BGREWRITEAOF
LASTSAVE

发布与订阅
PUBLISH
SUBSCRIBE
PSUBSCRIBE
UNSUBSCRIBE
PUNSUBSCRIBE
PUBSUB

复制
SLAVEOF
ROLE

客户端与服务器
AUTH
QUIT
INFO
SHUTDOWN
TIME
CLIENT_GETNAME
CLIENT_KILL
CLIENT_LIST
CLIENT_SETNAME

配置选项
CONFIG_SET
CONFIG_GET
CONFIG_RESETSTAT
CONFIG_REWRITE

调试
PING
ECHO
OBJECT
SLOWLOG
MONITOR
DEBUG_OBJECT
DEBUG_SEGFAULT

内部命令
MIGRATE
DUMP
RESTORE
SYNC
PSYNC
```



## Redis扩容和缩容

```shell
redis-cli --cluster
/usr/redis/bin/redis-cli --cluster add-node 192.168.212.163:7006   192.168.212.163:7000
cluster slots
/usr/redis/bin/redis-cli --cluster reshard  192.168.212.163:7000
```

## 缓存一致性

保证最终一致性方案是不行的，因过期时间造成了延时。给缓存设置过期时间，所有的写操作以数据库为准，只要到达缓存过期时间，则后面的读请求自然会从数据库中读取新值然后回填缓存。

### Scenario

### A.外部依赖

```css
(1)do sth
(2)Object = 调依赖接口、缓存、网络请求返回  // 存在失败的可能性
(3)Object Update
```

### B.缓存和DB一致性

#### 问题(1)先写缓存，后写DB

若先写缓存失败，直接返回，则无影响。

若先写缓存成功，后写DB失败，（1）数据库有旧值：此时若不清空缓存中写入的数据，则缓存中是新值，DB是旧值，数据不一致。（2）数据库没有旧值

#### 问题(2)若先写DB，后写缓存

若先写DB失败，直接返回，则无影响。

若先写DB成功，缓存写入失败，重试写入缓存也失败，则造成数据不一致，DB是新值，缓存旧值。解决方案：（1）缓存的key过期时间设短，到达过期时间，则后面的读请求自然会从DB中读取新值更新缓存，达到一致性。（2）任务持久化，异步去拿数据库的值更新缓存，但也存在重启或任务失败的问题。

#### 解决方案-读写分离+状态机（注意顺序）

读：读缓存，缓存读不到读DB，读到DB更新缓存。

写：删缓存旧的，写库，读库新值更新缓存。

#### 补充：数据库发生变化，如何及时更新缓存

```css
(1)每次更新完数据库都需调用类似刷新缓存方法
(2)实时同步(Aspect + 事件驱动异步) VS 分批按时间戳同步 
```

## 缓存失效策略

### 定时删除（内存友好）

设Key的过期时间，为Key设定时器，可保证内存释放快。但Key量大，每个Key都对应一个定时器，性能占CPU高。

### 惰性删除（CPU友好）

Key过期时间满不删，读库取Key检查过期？过期删除返回null：不过期返回Value

占CPU少，Key长时间不被获取就没被删，内存泄漏

### 缓存命中率

不命中情况：缓存不存在、已过期。

命中率高，性能好，响应时间短、吞吐量高，并发强。

高频低时效：预热、扩容、优化缓存粒度（粒度意思是大对象拆细分片，不拆redis集群有的数据小读取块，有的十分大读取非常慢占用更多的网络资源来序列化）、定时更新缓存提高命中率。

## 缓存雪崩、降级、穿透、预热

### 缓存雪崩

Scenario：（1）缓存集群重启（2）缓存的过期时间设置导致的集体失效（3）大查询流量去读库

Solution：（1）机架做HA（主从、大对象分片）、主从、扩展，开启AOF（灾备、误删）或RDB（全量数据恢复、快）（2）热度排序，高热度缓存过期时间设长、冷门设短，范围区间内随机设置过期时间（3）Encache（内存也备一份）+ hystrix

大对象比如2M以上的放redis，虽然Redis支持很大Value值，由于大对象序列化和反序列化要消耗更多的时间，大量请求下会阻塞，阻塞对后续的服务产生影响，有依赖关系的服务都受影响，大面积的阻塞最后导致雪崩

雪崩曲线：一般是由平缓急剧下降后再急剧上升。

### 缓存降级

Scenario：缓存集群挂掉、失效，也不读库，直接返回默认数据（写死、配置数据、读库）

Solution：热点数据双保险，一份内存，另一份缓存

### 缓存穿透

流程：查缓存—>缓存不存在读库

Scenario：恶意攻击或高并发请求查缓存没查到后读库，没命中率高导致穿透读库

Solution：数据库若也没有设一个key null也设置过期时间，滤重 bitmap效果明显比boomfilter好

### 缓存预热

Scenario：元数据提前预热加载到缓存，避免先查库

Solution：依据数据量（1）量小，放Apollo配置或工程启动时加载（2）量大，定时任务周期性刷新缓存（3）超量，分布式工程化提前加载

## 事务

```css
Redis不支持事务，Redis单个操作是原子性的。多个操作顺序执行不具备原子性，执行过程中中间失败话，不会回滚，还会继续执行。为什么不支持回滚？原子性的命令操作直观给出异常比负杂逻辑更清晰明了。事务回滚并不会解决程序Bug，只有当Redis命令有语法错误时才会执行失败，不支持回滚是让开发人员在开发期间就发现错误，尽早抛出错误。如何保证Redis执行多个操作不中断？Redis执行Lua脚本具原子性。
```

### 选型RDB VS AOF

RDB（全量数据、无法实时和秒级持久化、大数据量、夜深人静悄悄恢复、副本占2倍内存、数据完整性和一致性低）

RDB恢复数据比AOF快

AOF（写性能高、记录内容多、文件越来越大、数据恢复越来越慢、适合灾备误删除紧急恢复，但AOF占的快照比RDB大，开启AOF，写QPS下降，恢复数据慢，不适合冷备）

冷备（RDB）：关机离线备份。热备（AOF）：不关机，一般双机热备。

## 问题集

### Redis单个Key超过512M？

setrange命令证明、官网说明key最大是512M。单个value超过512M优化？

### 为什么RedisCluster有16384个槽？

16384=2的14次方

HASH_SLOT=CRC16(key) mod 16384

Normal heartbeat packets carry the full configuration of a node, that can be replaced in an idempotent way with the old in order to update an old config. This means they contain the slots configuration for a node, in raw form, that uses 2k of space with16k slots, but would use a prohibitive 8k of space using 65k slots.
At the same time it is unlikely that Redis Cluster would scale to more than 1000 mater nodes because of other design tradeoffs.
So 16k was in the right range to ensure enough slots per master with a max of 1000 maters, but a small enough number to propagate the slot configuration as a raw bitmap easily. Note that in small clusters the bitmap would be hard to compress because when N is small the bitmap would have slots/N bits set that is a large percentage of bits set.

若槽位Slot太大，发送心跳信息的消息头达8k，发送的心跳包过于庞大。e.g.如果是2的16次方作为Slot，65536÷8÷1024=8KB，8KB的消息头浪费带宽。槽位太小，bitmap的填充率Slots / N很高(N表示节点数)，bitmap的压缩率就很低。

```css
cluster info 查看当前集群信息
cluster nodes 查看集群各个节点负责的Slot
```

补Redis Slot流程图

节点数在1000以内够用：Redis的集群主节点数量基本不可能超过1000个。节点数在1000以内的redis cluster集群，16384个槽位足够用。

bitmap进行压缩高，槽位越小，节点少的情况下，压缩率高，bitmap的填充率slots / N很高的话(N表示节点数)：Redis主节点的配置信息中，哈希槽是通过一张bitmap的形式来保存的，bitmap进行压缩，但是如果bitmap的填充率slots / N很高的话(N表示节点数)，bitmap的压缩率就很低。

### CRC16 hash VS 一致性Hash

```css
一致性hash是一个0-2^32的闭合圆，有2^23个桶空间。

Redis Cluster划分为16383个Slot，不同key划分到不同Slot，Redis Cluster是作者antirez自己实现CRC16 hash算法，算法公式是HASH_SLOT = CRC16(key) mod 16384，Redis Cluster没有用一致性Hash。Codis是1024个Slot。
```

# HDFS

# Flume

# Kylin

# Storm(快被淘汰)

# Yarn



# Mesos



# Hibernate

# Mybatis VS JPA VS SpringData

```css
Mybatis移植需改SQL，JPA(是规范，SpringData JPA是框架)不关心数据库，迁移移植性好，SpringData是单表。
```

# Mybatis

## Mybatis Plugin(阿里面试题)



## Mybatis数据类型

```java
 1 Mybatis JDBC Type   Java Type  
 2 CHAR                String  
 3 VARCHAR             String  
 4 LONGVARCHAR         String  
 5 NUMERIC             java.math.BigDecimal  
 6 DECIMAL             java.math.BigDecimal  
 7 BIT             　　 boolean  
 8 BOOLEAN             boolean  
 9 TINYINT             byte  
10 SMALLINT            short  
11 INTEGER             int  
12 BIGINT              long  
13 REAL                float  
14 FLOAT               double  
15 DOUBLE              double  
16 BINARY              byte[]  
17 VARBINARY           byte[]  
18 LONGVARBINARY       byte[]  
19 DATE                java.sql.Date  
20 TIME                java.sql.Time  
21 TIMESTAMP           java.sql.Timestamp  
22 CLOB                Clob  
23 BLOB                Blob  
24 ARRAY               Array  
25 DISTINCT            mapping of underlying type  
26 STRUCT              Struct  
27 REF                 Ref  
28 DATALINK            java.net.URL[color=red][/color]  
```

## Mybatis  Plus update null

```java
BudgetCompare budgetCompare = budgetCompareMapper.selectById(budget.getId());
if (null == budgetCompare) {
    throw new CustomException(IcaCode.BUDGET_COMPARE_UPDATE_NOT_EXIST);
}
BeanUtils.copyProperties(budget, budgetCompare);
budgetCompare.setUpdater(userId);

UpdateWrapper updateWrapper = new UpdateWrapper();
updateWrapper.eq("id", budgetCompare.getId());
updateWrapper.eq("project_id", budgetCompare.getProjectId());
// 允许更新为null
updateWrapper.set(request.getCompareType() == null, "compare_type", null);
updateWrapper.set(request.getSelectType() == null, "select_type", null);
updateWrapper.set(budgetCompare.getFileUrl() == null, "file_url", null);
update(budgetCompare, updateWrapper);
```

## Mybatis Plus 删除和逻辑删除



## Mybatis where 1=1造成sql注入

```xml
<select id="findBookTypeListByExample" parameterType="BookType" resultMap="BookType">
    SELECT
        BOOK_TYPE_CODE, BOOK_TYPE_NAME, DISCOUNT
        FROM ASSETS_BOOK_TYPE
        WHERE 1=1
    <if test="BookTypeCode!=null">
        AND BOOK_TYPE_CODE = #{BookTypeCode,jdbcType=VARCHAR}
    </if>
    <if test="BookTypeName!=null">
        AND BOOK_TYPE_NAME = #{BookTypeName,jdbcType=VARCHAR}
    </if>
    <if test="Discount!=null">
        AND DISCOUNT = #{Discount,jdbcType=DECIMAL}
    </if>
</select>

<!--trim替换where--> 
<select id="findBookTypeListByExample" parameterType="BookType" resultMap="BookType">
	SELECT BOOK_TYPE_CODE, BOOK_TYPE_NAME, DISCOUNT FROM ASSETS_BOOK_TYPE
        <trim prefix="WHERE" prefixOverrides="AND |OR ">
            <if test="BookTypeCode!=null">
                BOOK_TYPE_CODE = #{BookTypeCode,jdbcType=VARCHAR}
            </if>
            <if test="BookTypeName!=null">
                AND BOOK_TYPE_NAME = #{BookTypeName,jdbcType=VARCHAR}
            </if>
            <if test="Discount!=null">
                AND DISCOUNT = #{Discount,jdbcType=DECIMAL}
            </if>
        </trim>
</select>

<!--where好处是不需要考虑where元素里的条件输出，(1)所有条件不满足MyBatis会查出所有记录(2) MyBatis会智能把首个and或or忽略，Ex.如BookTypeCode = null，BookTypeName!=null，则输出整个语句是SELECT BOOK_TYPE_CODE, BOOK_TYPE_NAME, DISCOUNT FROM ASSETS_BOOK_TYPE WHERE BOOK_TYPE_NAME = #{BookTypeName}，省略了首个and (3)where元素中不考虑空格，Mybatis会智能帮加上--> 
<select id="findBookTypeListByExample" parameterType="BookType" resultMap="BookType">
    SELECT
        BOOK_TYPE_CODE, BOOK_TYPE_NAME, DISCOUNT
        FROM ASSETS_BOOK_TYPE
    <where>
        <if test="BookTypeCode!=null">
            BOOK_TYPE_CODE = #{BookTypeCode,jdbcType=VARCHAR}
        </if>
        <if test="BookTypeName!=null">
            AND BOOK_TYPE_NAME = #{BookTypeName,jdbcType=VARCHAR}
        </if>
        <if test="Discount!=null">
            AND DISCOUNT = #{Discount,jdbcType=DECIMAL}
        </if>
	</where>
</select>
```

## Mybatis Plus分页

```

```

