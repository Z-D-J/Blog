---
title: Redis
date: 2021-01-30 11:09:31
tags:
---

# Redis概念

* redis是一款高性能的NOSQL系列的非关系型数据库。
  * Redis（Remote Dictionary Server )，即远程字典服务，是一个开源的使用ANSI C语言编写、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。
  * Redis支持的键值数据类型：
    1. String:字符串类型;
    2. hash:哈希类型;
    3. list：列表类型;
    4. set：集合类型;
    5. sortedset:有序集合类型。
  * Redis的应用场景：
    1. 数据缓存（数据查询，短链接，新闻内容，商品内容等）
    2. 聊天室的在线好友列表;
    3. 任务队列（秒杀，抢购，12306的高并发等）
    4. 应用排行榜;
    5. 数据过期处理;
    6. 分布式集群架构中的session分离
* NOSQL:Not Only SQL ,泛指非关系型数据库。
  * 为了应对大规模数据的挑战。
* 关系型数据库：
  * 数据之间有关联关系。
  * 数据存储在硬盘的文件中。
  * 数据以表的形式存储。
* 非关系型数据库，
  * 数据之间没有关系;
  * 数据存储在内存中;
  * 存储格式有key:value形式，文档形式，图片形式等。
* 主流NOSQL产品：
  * 键值（key:value)数据库：
    * Tokyo Cabinet/Tyrant， Redis， Voldemort， Oracle BDB
    * 应用场景：内容缓存，主要用于处理大量数据的高访问负载，也用于一些日志系统等等。
    * 数据模型：Key 指向 Value 的键值对，通常用hashtable来实现
  * 列存储数据库：
    * Cassandra， HBase， Riak
    * 应用场景：分布式的文件系统
    * 数据模型：以列簇式存储，将同一列数据存在一起
  * 文档型数据库：
    * CouchDB， MongoDb
    * 应用场景：Web应用（与Key-Value类似，Value是结构化的，不同的是数据库能够了解Value的内容）
    * 数据模型：Key-Value对应的键值对，Value为结构化数据
  * 图形(Graph)数据库：
    * Neo4J， InfoGrid， Infinite Graph
    * 应用场景：社交网络，推荐系统等。专注于构建关系图谱
    * 数据模型：图结构。

# Redis的安装

* 下载：[官网](https://redis.io),[中文网](https://www.redis.net.cn)
* 为linux系统下载的`.tar.gz`文件，通过`tar -xzf`命令解压缩;
* 进入解压缩文件目录下，执行`make`编译该文件