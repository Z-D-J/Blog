---
title: Hadoop
date: 2020-10-26 18:31:15
tags:
---

# Hadoop简介

* Hadoop是由Apache基金会所开发的**分布式系统基础架构**。
* 主要解决问题：
  1.  海量**数据的存储**；
  2.  海量**数据的分析计算问题**。
* Hadoop生态圈：包含Hadoop框架以及nutch等。
* Hadoop的三大发行版本：
  1. Apache:原始版本，适用于入门学习。
  2. Cloudera：在大型互联网企业中使用。（又叫CDH版）
  3. Hortonworks：文档较好。
* Hadoop的优势：
  1.  高可靠性：Hadoop维护了**多个数据副本**（在多个服务器上），即使Hadoop某个计算元素或存储出现故障，也不会导致数据的丢失。
  2.  高扩展性：在**集群间分配**任务数据，可方便的扩展数以千计的节点（服务器）。
  3.  高效性：基于MapReduce思想，**并行**工作，加快任务处理速度。
  4.  高容错性：能够自动将**失败的任务重新分配**。
* Hadoop组成
  * Hadoop1.x：
    1.  common（辅助工具）：
    2.  HDFS（数据存储）：
    3.  MapReduce（计算+资源调度）：
  * Hadoop2.x：
    1.  common（辅助工具）：
    2.  HDFS（数据存储）：
    3.  Yarn(资源调度)：
    4.  MapReduce（计算）：

# Hadoop组成概述

## HDFS架构概述

1.  NameNode（nn):存储文件的**元数据**，如文件名，文件目录结构，文件属性，以及每个文件的块列表和所在的DataNode等。（相当于一个目录，真正的数据在DataNode中。）
2.  DataNode(dn):在本地文件系统存储**文件块数据**，以及块数据的检验和。
3.  Secondary NameNode（2nn）：用来**监控HDFS状态**的辅助后台程序。

## Yarn架构概述

![IMG_2177](https://gitee.com/zhangjie0524/picgo/raw/master/uPic/IMG_2177.JPG)
* ResourceManger(RM：**整个资源管理**老大)主要作用：
  1.  处理客户端请求
  2.  监控NodeManger
  3.  启动或监控ApplicationMaster(任务管理)
  4.  资源的分配与调度。
* NodeMaster（NM：节点老大）作用：
  1. 管理**单个节点**上的资源。
  2. 处理来自ResourceManger的命令。
  3. 处理来自ApplicationManager命令。
* ApplicationManger（AM：任务老大）作用：
  1. 负责**数据**的切分。
  2. 为应用程序申请资源并分配给内部的任务。
  3. 任务的监控与容错。
* Container
  * Container是yarn中的**资源抽象**，它封装了某个节点（可理解为一台电脑）上的多个维度资源，如内存，cpu，磁盘，网络等。

## MapReduce架构概述

* MapReduce将计算过程分为两个阶段：Map和Reduce（先分后合）：
  1. Map阶段**并行处理**输入数据（将运算任务分给不同的服务器）；
  2. Reduce阶段对Map的阶段的结果进行**汇总**。

## 大数据技术生态
  
* 大数据技术生态图：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201027094308.png)

# Hadoop运行环境搭建

