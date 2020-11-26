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

## 1.导入驱动jar包到项目目录下

1. mysql的jar包下载:[官网](https://dev.mysql.com/downloads/connector/);下载时选择platformIndependent
2. 复制jar包到项目的libs目录下（也可以直接导入），右键->add as library
## 2. 注册驱动

* `  Class.forName("com.mysql.jdbc.Driver");`,会产生ClsaaNotFoundException的异常。

## 3. 获取数据库的连接对象

* `Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/youth_study", "root","root");`
  * 参数依次为连接地址，用户名，密码。
  * 连接地址中，后面是主机名：端口/数据库名

## 4.定义sql

* `String sql = "update t_branch set college_id = 2 where id = 1";`,定义一个存储sql语句的字符串。

## 5.获取执行sql语句的对象

*  `Statement  stmt = conn.createStatement();`conn是数据库的连接对象。
## 6.执行sql，接受返回结果；

* ` int count = stmt.executeUpdate(sql);`
* ` System.out.println(count);`

## 7. 释放资源

* `conn.close();`
* `stmt.close();`

# JDBC对象
