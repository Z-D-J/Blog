---
title: Hadoop
date: 2020-10-26 18:31:15
tags:
---

# Hadoop简介

* Hadoop是由Apache基金会所开发的分布式系统基础架构。
* 主要解决问题：
  1.  海量数据的存储；
  2.  海量数据的分析计算问题。
* Hadoop生态圈：包含Hadoop框架以及nutch等。
* Hadoop的三大发行版本：
  1. Apache:原始版本，适用于入门学习。
  2. Cloudera：在大型互联网企业中使用。（又叫CDH版）
  3. Hortonworks：文档较好。
* Hadoop的优势：
  1.  高可靠性：Hadoop维护了多个数据副本（在多个服务器上），即使Hadoop某个计算元素或存储出现故障，也不会导致数据的丢失。
  2.  高扩展性：在集群剪分配任务数据，可方便的扩展数以千计的节点（服务器）。
  3.  高效性：并行工作，加快任务处理速度。
  4.  高容错性：能够自动将失败的任务重新分配。
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

1.  NameNode（nn):存储文件的元数据，如文件名，文件目录结构，文件属性，以及每个文件的块列表和所在的DataNode等。（相当于一饿目录，真正的数据在DataNode中。）
2.  DataNode(dn):在本地文件系统存储文件块数据，以及块数据的检验和。
3.  Secondary NameNode（2nn）：用来监控HDFS状态的辅助后台程序。

## Yarn架构概述

![IMG_2177](https://gitee.com/zhangjie0524/picgo/raw/master/uPic/IMG_2177.JPG)
