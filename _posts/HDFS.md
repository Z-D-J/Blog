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

# HDFS基本概念

## 数据块(Block)

* HDFS的文件是以数据块存储的，数据块是HDFS文件处理的**最小单元**。
* HDFS的数据块很大，默认为每块**128MB**。
* HDFS**数据块会以文件**的形式存储在数据节点的磁盘上。
* HDFS中所有文件都会被**切分成若干个数据块**分布在数据节点上存储。
* HDFS会将同一个数据块**冗余备份**到不同的数据节点上(一个数据块默认保存**3份**)。

## 名字节点(NameNode)

* NameNode是HDFSMaster/Slave结构中的**主节点**。
* NameNode管理文件系统**命名空间(NameSpace)**以及**数据块和数据节点之间的对应关系**。
  * NameSpace:
    * 包括**文件系统目录树**，**文件目录信息**，以及**文件的数据块索引**（文件->数据块）；
    * 这些信息以**命名空间镜像文件**和**编辑日志文件**这两个文件的形式**永久的保存在NameNode的本地磁盘上**。
  * 数据块与数据节点之间的对应关系：
    * 并不保存在NameNode的本地磁盘上，而是在NameNode启动时**动态构建**。
* NameNode是HDFS的**单一故障点**，如果NameNode丢失元数据或者损坏，文件系统将出现错误。
  * Hadoop 2.X版本引入**名字节点高可用性(HA)**,来解决这个问题：
* NameNode中要保存数据块与数据节点之间的对应关系，如果文件数量过多，**NameNode的内存将成为限制系统横向扩展的瓶颈**。
  * Hadoop 2.X版本引入**联邦HDFS机制(HDFS Federation)**,来解决这个问题。

## 数据节点(DataNode)

* DataNode是HDFS的**从结点**;
* DataNode会根据Client的请求和NameNode的指令来从本地存储中读取数据块，或者向本地存储中写入数据块。
* DataNode会不断向NameNode发送**数据块汇报，心跳和缓存汇报**。

## 客户端(client)

* HDFS提供了多种客户端接口供**应用程序**和**用户**使用，这些接口包括**命令行接口**，**浏览器接口**和**代码API接口**。

## HDFS通信协议

* HDFS的使用流程需要client，NameNode，DataNode三者之间的配合和相互调用。HDFS将这些节点间的调用抽象成不同的**接口**。
* HDFS节点间的接口主要有两种类型：
  1. Hadoop RPC接口
  2. 流式接口

# Hadoop RPC接口

* Hadoop RPC接口是基于Protobuf实现的，主要定义在`org.apache.hadoop.hdfs.protocol`包和`org.apache.hadoop.hdfs.server.protocol`包中、
* Hadoop RPC接口主要包含以下几个接口：
  1. **ClentProtocol**:这个接口定义了**client和NameNode**之间的接口，clent对文件的所有操作都要通过这个接口。
  2. **ClientDatanodeProtocol**:这是**client和DataNode**之间的接口，其中的方法是在**client获取DataNode的信息时调用**，而不是直接的数据读写交互。
  3. **DatanodeProtocol**:DataNode通过这个接口和**NameNode通信**，同时NameNode通过这个接口中方法的返回值向DataNode下发指令，这个接口是**DataNode和NameNode之间通信的唯一方式**。
  4. **InnerDatanodeProtocol**:这是**DataNode和DataNode之间通信的接口**，这个接口主要用于**数据块的恢复操作，以及同步DataNode上存储的数据块副本的信息**。
  5. **NameNodeProtocol**: **Secondary NameNode和NameNode之间的接口**，如果引入了HA机制，则不使用Secondary NameNode，这个接口作用有限。
  6. 其它接口：如安全相关接口，HA相关接口。

## ClientProtocol

### 读数据相关方法

* `getBlockLocations()`:客户端调用该方法获取指定范围内所有**数据块的位置信息**。
  * 参数：HDFS文件的**文件名**和**读取范围**。
  * 返回值：文件指定范围内所有数据块的文件名以及它们的位置信息，用**LocatedBloclks对象**封装。
    * 数据块的位置信息是指所有存储这个数据块副本的DataNode信息，这些DataNode会以与当前客户端的距离远近排序。
  * 定义：`public LocatedBlocks getBLockLocations(String src, long offset,long length);`