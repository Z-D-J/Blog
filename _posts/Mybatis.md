---
title: Mybatis
date: 2021-02-08 22:23:17
tags:
---

# Mybatis简介

* MyBatis 是一款优秀的**持久层框架**。
  * 持久化：将程序的数据永久存储到硬盘上；
  * 持久层：完成持久化工作的代码块，即三层架构中的**DAO层**。
* MyBatis 避免了几乎所有的JDBC代码和手动设置参数以及获取结果集。
* MyBatis 可以使用简单的 **XML 或注解来配置和映射原生信息**，将接口和 Java 的 POJOs(Plain Ordinary Java Object,普通的 Java对象)映射成数据库中的记录。
* Mybatis资料：
  * [官方文档](https://mybatis.org/mybatis-3/zh/index.html)
  * [下载地址](https://github.com/mybatis/mybatis-3/releases)
  * maven坐标：
```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.6</version>
</dependency>
```
* 优点：
  * 简单易学：本身就很小且简单。没有任何第三方依赖，最简单安装只要两个jar文件+配置几个sql映射文件。
  * 灵活：mybatis不会对应用程序或者数据库的现有设计强加任何影响。 **sql写在xml里**，便于统一管理和优化。通过sql语句可以满足操作数据库的所有需求。
  * 解除sql与程序代码的耦合：通过提供DAO层，将业务逻辑和数据访问逻辑分离。
  * 提供xml标签，支持编写动态sql。

# 快速入门

## 一：环境搭建

1. 通过maven导入三个jar包：
   1. mysql驱动包：
   2. junit包；
   3. mybatisjar包
```xml
    <dependencies>
        <!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.23</version>
        </dependency>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13</version>
            <scope>test</scope>
        </dependency>>
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.6</version>
        </dependency>
    </dependencies>
```