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

# Docker的使用