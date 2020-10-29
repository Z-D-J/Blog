---
title: Mysql
date: 2020-10-23 12:09:42
tags:
---

# 数据库简介

* 特点：
  1.  持久化保存数据；
  2.  可以实现结构化查询，方便管理。
* DB:数据库（database），存储数据的仓库，保存了有组织的数据。
* DBMS:数据库管理系统。数据库是通过DBMS来创建和管理的容器。常见数据库管理系统：MYSQL，Oracle，DB2,SqlServer。
* SQL：结构化查询语言（StructureQuery Language），专门用来与数据库通信。几乎所有DBMS都支持SQL。
* 数据存储数据：
  1.  将数据存入表中，表再放入库中。一个数据库中可以有多个表，每个表有一个名字，表名具有唯一性。
  2.  表具有一些特性，这些特性定义了数据在表中如何存储，类似java中的“类”。
  3.  表由列组成，这些列也称为**字段**，每一列类似java中的属性。
  4.  表中的数据是按行存储的，每一行类似java中的对象。

# MySQL的安装

* MySQL的特点：
  1.  开放源代码；
  2.  性能高
  3.  容易安装和使用。
* DBMS的分类：
  1.  基于共享文件系统的（如：Access）
  2.  基于客户机-服务器的DBMS（如；MySQL，oracle，sqlsever）。
* MySQL下载安装：
  1.  社区版（免费）
  2.  企业版（收费）
  3.  下载地址：https://dev.mysql.com/downloads/installer/
  4.  跟随安装指导进行配置。

# MySQL服务的启动

1. 搜索服务，点击打开；
2. 在cmd输入`services.msc`启动；
3. 在管理员cmd输入`net start <本机mysql的名字>`或者`net stop <本机mysql的名字>`启动或者关闭。

# MySQL的登录

* 登录本地用户：`mysql -uroot -proot`，-u后面接的是用户名，-p后面接的是root用户的密码。`mysql -uroot -p`,会在之后输入密码。
* 登录远程用户：`mysql -h127.0.0.1 -p` -h后面接的是连接目标的ip。
* 登录：`mysql --host=IP --user=用户名 --passward=连接目标的密码`

# MySQL的目录结构

1.MySQL的安装目录：
  1.  bin：二进制可执行文件，包括很多命令的执行程序。
  2.  data：存放mysql的日志文件，数据文件等。
  3.  include：放置.h头文件；
  4.  lib：所需的jar包；
  5.  share：错误信息存放
2.MySQL的数据目录：（在c盘下的programdata下）
  1.  数据库及其中的数据；
  2.  my.ini是MySQL的配置文件。

# SQLyog图形化界面

* 可以使用sql语句控制，也可以直接使用鼠标控制。

# SQL语句

## SQL的简介

* SQL：结构化查询语言（StructureQuery Language），专门用来与数据库通信。几乎所有DBMS都支持SQL。可以用来操作所有的关系型数据库。

## SQL的通用语法

* SQL可以单行或者多行书写，以分号结尾。
* 使用空格和缩进来规范格式。
* Mysql的SQL语句不区分大小写。，关键字建议使用大写。
* 注释：
  1.  单行注释：`-- `或者`# `之后写注释内容。（--注释符后面有空格。#可以没有空格，是MySQL特有的。）

## SQL的分类

* DDL（data definition language）：操作数据库和表；
* DML（Data Manipulation Language）；增删改表中的数据。
* DQL（Data Query Language）:查询表中的数据。
* DCL（Data control Language）:数据控制语言，控制访问权限和安全级别等。

## DDL

### 操作数据库（CRUD）

1. C（creat）:创建；
   1. 创建数据库：`creat database 数据库名称;`
   2. 判断数据库不存在，再创建：`creat database if not exists 数据库名称;`
   3. 创建数据库，并指定字符集：`creat database 数据库名称 character set 字符集名;`
2. R（Retrieve）：查询；
   1. 查询已经存在的数据库：`show databases;`
   2. 查看某个数据库的字符集：`show creat database 数据库名称;`(同时也是查询数据库的创建语句)
3. U（Update）：修改；
   1. 修改数据库的字符集：`alter database 数据库名称 character set 字符集名称;`
4. D(Delete):删除；
   1. 删除数据库：`drop database 数据库名称;`。
   2. 判断数据库存在，再删除：`drop database if exists 数据库名称;`
5. 使用数据库。
   1. 查询当前正在使用的数据库名称:`select database();`
   2. 使用数据库：`use 数据库名称;`

### 操作表（CRUD）


1. C（creat）:创建；
   1. 创建语法:`creat table 表名（列名1， 数据类型1， 列名2 数据类型2， ... 列名n 数据类型n）;`**创建表时，至少有一个列，否则创建会直接失败**
   2. 复制：`creat table 表名（即将创建） like 表名（被复制的）`
2. R（Retrieve）：查询；
   1. 查询数据库中所有表的名称：`show tables;`
   2. 查询表结构：`desc 表名;`
3. U（Update）：修改；
   1. 修改表名：`alter table 表名 rename to 新表名;`
   2. 修改表的字符集：`alter table 表名 character set 字符集名称;`
   3. 添加一列：`alter table 表名 add 列名 数据类型;`
   4. 修改列名称 类型：`alter table 表名 modify 列名 新数据类型;`（仅修改列的数据类型）或者`alter table 表名 change 列名 新列名 新数据类型;`
   5. 删除列：`alter table 表名 drop 列名;`
4. D(Delete):删除；
   1. 删除数据库中的表;·drop table 表名;`
   2. 判断表存在后再修改:`drop table if exists 表名;`

### 数据类型

* int： 整数类型；
* double：浮点数类型，double（5, 2）表示总共有5位数，其中小数点后有两位。
* date:日期，只包含年月日，yyyy-mm-dd;
* datetime:日期，包含年月日时分秒，yyyy-mm-dd HH:mm:ss;
* timestamp:时间戳类型，包含年月日时分秒（同datetime），但是如果不给这个字段赋值或者赋值为null，则默认使用当前的系统时间来自动赋值。
* varchar：字符串类型，varchar（20），表示字符串的最多有20个字符。**必须在varchar后面接上（数字），否则就是语法错误。**

## DML

1. 添加数据：
   1. 添加语法：`insert into 表名 （列名1， 列名2，... ，列名n）value（值1，值2，...,值n）;`
      1. 列名和值要一一对应；
      2. 如果表名后不给列名，在提供和列数相同个数值的前提下，会默认依次给所有列添加值，否则会报错。