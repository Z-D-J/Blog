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

* 是Client发起调用的接口。
### 读数据相关方法

* `getBlockLocations()`:客户端调用该方法获取指定范围内所有**数据块的位置信息**。
  * 参数：HDFS文件的**文件名**和**读取范围**。
  * 返回值：文件指定范围内所有数据块的文件名以及它们的位置信息，用**LocatedBloclks对象**封装。
    * 数据块的位置信息是指所有存储这个数据块副本的DataNode信息，这些DataNode会以与当前客户端的距离远近排序。
  * 定义：`public LocatedBlocks getBLockLocations(String src, long offset,long length);`
  * 使用：client会首先调用`getBlockLocations()`方法获取文件的所有数据块的位置，然后根据这些**位置信息**从DataNode读取数据块。
* `reportBadBlocks()`:客户端调用该方法向NameNode汇报错误的数据块。
  * 参数：LocatedBlock对象数组
  * 定义：`public void reportBadBlocks(LocatedBlock[]  blocks);`
  * 使用： 当client从DataNode**读取数据块并且发现数据块的校验和并不正确时**，调用这个方法向NameNode汇报这个错误数据块的信息。

### 写/追加写数据相关方法

* `creat()`:用于在HDFS文件系统目录树中创建一个新的空文件。
  * 参数：由`String src`参数指定创建文件的路径。
  * 返回值：
  * 定义:`public HDFSFileStatus create(String src,...(此处省略后续参数));`
* `append()`:用于打开一个已有的文件。
  * 如果这个文件的**最后一个数据块没有写满**，则返回这个数据块的位置信息(用LocatedBlock对象封装);
  * 如果这个文件的**最后一个数据块恰好写满**，则**创建一个新数据块**并添加到这个文件中，然后返回这个新添加数据块的位置信息。
  * 定义:`public LocatedBlock append(String src, String clientName);`
* `addBlock()`:向指定文件**添加一个新数据块**，并获取存储这个数据块副本的所有**DataNode的位置信息**。
  * 调用该方法需要传入**上一个数据块的引用**（即previous参数）；
  * excludeNodes参数：是DataNode的黑名单，保存了client**无法连接的一些DataNode**；
  * favoredNodes参数：是client希望保存数据块副本的**DataNode列表**.
  * 定义：`public LocatedBlock addBlock(String src, String clientName, ExtenedNode previous, DataNodeInfo[] excludeNodes, long fileId,  String[] favoredNodes);`
* `complete()`:当客户端**完成了整个文件的写入操作后**，会调用该方法**通知NameNode**。
  * 该方法会**提交所有新写入的数据块信息**；
  * 当该文件的**所有数据块至少都有一个副本**时，该方法会返回true,这时NameNode中文件的状态也会从**构建中状态转换为正常状态**；
  * 否则，该方法返回false，**client需要反复调用`complete()`方法,直到返回ture。
  * 定义：`public boolean complete(String src, String clientName, ExtendedBlock last, long fileId);`
* 正常写新文件流程：
  1. client调用`create`方法在文件系统目录树上**创建一个空文件**；
  2. client调用`addBlock`方法获取存储文件的**数据块的位置信息**；
  3. client根据数据块的位置信息构建**数据流管道，向DataNode中写入数据**；
  4. client完成数据的写入，调用`complete`方法**通知NameNode**。
* 正常追写数据流程：
  1. client调用`append`方法**获取最后一个可写数据块的位置信息**；
  2. client根据该数据块的位置信息构建**数据流管道，向这个未写满的DataNode中写入数据**；
  3. client如果将原文件的最后一个数据块写满了，则调用`addBlock`方法获取存储文件的**数据块的位置信息**；
  4. client根据数据块的位置信息构建**数据流管道，向DataNode中写入数据**；
  5. client完成数据的写入，调用`complete`方法**通知NameNode**。  

### 对命名空间的管理相关方法

* HDFS对NameNode信息的修改的相关方法与FileSystem类抽象的所有方法。
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201216103550.jpg)

### 系统问题与管理操作

* ClientProtocol支持**DFSAdmin工具（供HDFS管理员管理HDFS集群的命令行工具）**的接口方法。
* 典型的dfsadmin命令：`hdfs dfsadmin[参数]`;
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201216135353.jpg)
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201216135358.jpg)
* **安全模式**：
  * 安全模式是NameNode的一种状态，处于安全模式的NameNode不接受client对NameSpace的修改操作，NameSpace处于**只读状态**。同时，NameNode也不会**向DataNode下发任何数据块的复制，删除操作**。
  * 刚刚启动的NameNode会**自动进入安全模式**。

### 快照操作

* 快照保存了HDFS在一个时间点某个路径中所有数据的拷贝；
* 快照可以将集群回滚到之间的一个正常的时间点上。
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201217151155.jpg)

### 缓存操作

* 集中式缓存管理功能：用户可以指定一些经常使用的数据或者高优先级任务的数据，使它们常驻缓存而不被淘汰到磁盘上。
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201217151806.jpg)

### 其它操作

* 如安全相关或者XAtrr相关命令

## ClientDatanodeProtocol

* ClientDatanodeProtocol定义了client和Datonode之间的接口，由client发起调用。
* `getRepublicaVisibleLength()`:用于从某个DataNode获取某个数据块副本真实的数据长度。
* `getBlockLocalPathInfo();`:client调用该方法获取指定数据块文件以及数据块校验文件在当前DataNode（和client一个物理机）上的本地路径。
* `refreshNamenodes()`:用于触发指定的DataNode重新加载配置文件，停止服务那些已经从配置文件中删除的块池，开始服务新添加的块池。
* `deleteBlockPool();`:用于从指定的DataNode删除指定的块池。
* `getHdfsBlocksMetadata();`:获取是存储在指定的DataNode的哪个卷上的。
* `shutdownDatanode();`:用于关闭一个数据节点。
* `getDatanodeInfo();`:获取指定的DataNode的信息：DataNode运行和配置的HDFS版本，以及DataNode的启动时间等信息。
* `startReconfiguration();`:触发DataNode异步地从磁盘加载并应用配置。
* `getReconfigurationStatus();`:用于查询上一次触发的重新加载配置操作的运行情况。

## DatanodeProtocol

* 