---
layout: w
title: docker
date: 2020-11-23 16:34:04
tags:
---

# Docker概述

[参考教程](https://www.runoob.com/docker/docker-tutorial.html)
* Docker 是一个开源的应用容器引擎，基于 Go 语言 并遵从 Apache2.0 协议开源。
* Docker的应用场景：
  * Web 应用的自动化打包和发布。
  * 自动化测试和持续集成、发布。
  * 在服务型环境中部署和调整数据库或其他的后台应用。
  * 从头编译或者扩展现有的 OpenShift 或 Cloud Foundry 平台来搭建自己的 PaaS 环境。

## Docker架构

* Docker 包括三个基本概念:
  * 镜像（Image）：Docker 镜像（Image），就相当于是一个 root 文件系统。比如官方镜像 ubuntu:16.04 就包含了完整的一套 Ubuntu16.04 最小系统的 root 文件系统。
  * 容器（Container）：镜像（Image）和容器（Container）的关系，就像是面向对象程序设计中的类和实例一样，镜像是静态的定义，容器是镜像运行时的实体。容器可以被创建、启动、停止、删除、暂停等。
  * 仓库（Repository）：仓库可看成一个代码控制中心，用来保存镜像。
* Docker 使用客户端-服务器 (C/S) 架构模式，使用远程API来管理和创建Docker容器。
* Docker 容器通过 Docker 镜像来创建。容器与镜像的关系类似于面向对象编程中的对象与类。

# Docker安装

[参考资料](https://www.runoob.com/docker/ubuntu-docker-install.html)

# Docker的基础使用

## 运行helloworld

* 命令：`docker run ubuntu:15.10 /bin/echo "Hello world"`
  * docker: Docker 的二进制执行文件。
  * run: 与前面的 docker 组合来运行一个容器。
  * ubuntu:15.10 指定要运行的镜像，Docker 首先从本地主机上查找镜像是否存在，如果不存在，Docker 就会从镜像仓库 Docker Hub 下载公共镜像。
  * /bin/echo "Hello world": 在启动的容器里执行的命令。
* 以上命令完整的意思可以解释为：Docker 以 ubuntu15.10 镜像创建一个新容器，然后在容器里执行 bin/echo "Hello world"，然后输出结果。

## 运行交互式容器

* 我们通过 docker 的两个参数 -i -t，让 docker 运行的容器实现"对话"的能力；
  * -t: 在新容器内指定一个伪终端或终端。
  * -i: 允许你对容器内的标准输入 (STDIN) 进行交互。
* 命令示例：`docker run -i -t ubuntu:15.10`，-i，-t两个参数必须同时使用，如果只使用-t则会只有一个终端界面，但是输入命令不会有反应。
* 我们可以通过运行 exit 命令或者使用 CTRL+D 来退出容器。

## 启动容器（后台模式）

* 命令:`docker run -d ubuntu:15.10 /bin/echo "helloworld"`
  * 在输出中，我们没有看到期望的 "hello world"，而是一串长字符串2b1b7a428627c51ab8810d541d759f072b4fc75487eed05812646b8534a2fe63。这个长字符串叫做容器 ID，对每个容器来说都是唯一的，我们可以通过容器 ID 来查看对应的容器发生了什么。
* 确认容器有在运行，可以通过 docker ps 来查看：
  * 输出详情介绍：
    * CONTAINER ID: 容器 ID。
    * IMAGE: 使用的镜像。
    * COMMAND: 启动容器时运行的命令。
    * CREATED: 容器的创建时间。
    * STATUS: 容器状态。
      * 状态有7种：
        * created（已创建）
        * restarting（重启中）
        * running 或 Up（运行中）
        * removing（迁移中）
        * paused（暂停）
        * exited（停止）
        * dead（死亡）
    * PORTS: 容器的端口信息和使用的连接类型（tcp\udp）。
    * NAMES: 自动分配的容器名称。
* 在宿主主机内使用 docker logs 命令，查看容器内的标准输出：
  * 示例：`docker logs 2b1b7a428627`(这串数字是容器id的前面一部分)
* 我们使用 docker stop 命令来停止容器：
  * 示例：`docker stop 2b1b7a428627`