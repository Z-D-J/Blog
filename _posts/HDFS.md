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

* 