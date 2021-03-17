---
title: hdfs源码解析
date: 2021-03-16 16:44:31
tags:
---

# hadoop源码编译安装

* 源码编译安装原因：
  * 适配不同平台的Native Libarary本地库；
  * 源码修改之后需要重新编译安装。
* 源码下载：
  * [官网](https://archive.apache.org/dist/hadoop/common/)
  * [镜像源](http://mirrors.hust.edu.cn/apache/)
* 源码中有官方对编译安装的说明文件Building.txt:
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/20210316172624.png)

## Ubuntu中源码编译

* 安装gcc:`sudo apt-get install gcc`
* 安装make：`sudo apt-get install make`
* 安装jdk1.8
* 安装maven
* 安装本地库：`sudo apt-get -y install build-essential autoconf automake libtool cmake zlib1g-dev pkg-config libssl-dev libsasl2-dev`
* 安装Cmake最新版：[下载地址](https://cmake.org/download/)
  * 下载源码，编译安装（进入到源码所在目录）
  ```shell
  ./bootstrap
  make
  sudo make install
  ```
* 安装Protocol Buffers:[下载地址](https://github.com/protocolbuffers/protobuf/releases)
  * 下载源码，编译安装(进入到源码所在目录)：
  ```shell
  sh autogen.sh
  ./configure --prefix=/usr/local
  make # 可以使用make -j8指定多线程编译（不一定是8）
  sudo make install
  ```
<!-- * 安装snappy：[下载地址](https://github.com/KnpLabs/snappy/releases/tag/v1.2.1)
  * 下载源码，编译安装（进入到源码所在目录）
  ```shell
  ./configure
  make
  sudo make install
  ``` -->
* 安装isa:[下载地址](https://github.com/intel/isa-l/releases)
```shell
apt-get install yasm
apt-get install nasm

# 进入isa源码目录下

sh autogen.sh
./configure
make 
sudo make install
```
* 安装zstd：[下载地址](https://github.com/facebook/zstd/releases)
```shell
# 进入源码目录下直接可以make
make
sudo make install
```
* 安装fuse：`sudo apt-get install fuse libfuse-dev`
* 将这些都准备好后，在idea中打开hadoop的hdfs模块，使用maven安装：
![](https://gitee.com/zhangjie0524/picgo/raw/master/20210317005112.png)

# HDFS源码工程结构

* hadoop中HDFS工程模块如图：
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/20210316215444.png)
* `hadoop-hdfs`：
  * 该模块提供整个HDFS的核心功能，是hdfs工程的核心模块。
* `hadoop-client`:
  * 该模块提供hdfs客户端的功能实现；
* `hadoop-hdfs-httpfs`:
  * 该模块主要实现了通过HTTP协议操作访问hdfs文件系统的相关功能；
  * HttpFS是一种服务器，它提供了HDFS的REST HTTP网关，具有完整的文件系统读写能力；
  * HttpFS可用于在不同的hadoop版本的集群之间传输数据。
* `hadoop=hdfs-native-client`:
  * 该模块定义了hdfs访问本地库的相关功能和逻辑；
  * 该模块主要使用c语言进行编写，用于和本地库进行交互操作。
* `hadoop-hdfs-nfs`:
  * 该模块是Hadoop HDFS的NFS实现；
  * NFS是指网络文件系统，能使使用者访问网络上别处的文件就像在使用自己的计算机一样。
* `hadoop-hdfs-rbf`:
  * 该模块主要实现了RBF功能；
  * RBF是Router-based Federation的简称，即基于路由的Federation方案。
