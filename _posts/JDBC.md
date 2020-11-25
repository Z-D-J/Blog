---
layout: w
title: JDBC
date: 2020-11-25 17:17:57
tags:
---

# JDBC概念

* JDBC是java database connectivity的缩写。是使用java语言来操作数据库。JDBC实现了使用统一的java代码来操作所有关系型数据库。
* JDBC是sun公司定义的操作所有关系型数据库的规则，即定义了一套接口。
* 每一个数据库厂商实现JDBC接口来操作自己的数据库。这些实现类的jar包就叫做**数据库驱动**。

# JDBC基本使用

1. 导入驱动jar包到项目目录下；
2. 注册驱动；
3. 获取数据库的连接对象；
4. 定义sql；
5. 获取执行sql语句的对象；
6. 执行sql，接受返回结果
7. 释放资源。