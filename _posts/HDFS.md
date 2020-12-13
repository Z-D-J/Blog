---
title: HDFS
date: 2020-12-13 22:00:43
tags:
---

# HDFS概述

* HDFS，即Hadoop分布式文件系统，是可以运行在通用硬件上，提供流式数据操作，能够处理超大文件的分布式文件管理系统。
* HDFS有高度容错，高吞吐量，高可靠性，容易扩展等特性。

# HDFS的体系结构

* HDFS是一个主从(Master/Slave)体系结构的分布式系统。
* 体系结构如图；
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201213221011.jpg)
* **NameNode**是HDFS的Master节点，负责管理文件系统的**命名空间(namespace)**,以及**数据块到具体DataNode的映射**等信息。
* **DataNode**一般是一个节点上一个，负责管理它所在节点上的存储。
* 用户与HDFS的交互：
  1. 用户能够通过**HDFS客户端(client)**,发起**读写**HDFS文件的请求，同时还能通过client执行HDFS命名空间的操作，如**打开，关闭，重命名文件或者目录**。
  2. **NameNode会响应客户端的请求**，来更改命名空间的信息以及DataNode和数据块的映射关系；
  3. NameNode会指导**DataNode来处理client的文件读写请求**。