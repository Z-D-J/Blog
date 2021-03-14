---
title: Spring Boot
date: 2020-09-20 15:29:43
tags:
---

# SpringBoot简介

* Spring Boot是由Pivotal团队提供的全新框架，其设计目的是用来简化新Spring应用的初始搭建以及开发过程。该框架使用了特定的方式来进行配置，从而使开发人员不再需要定义样板化的配置。
* SpringBoot所具备的特征有：
（1）可以创建独立的Spring应用程序，并且基于其Maven或Gradle插件，可以创建可执行的JARs和WARs；
（2）内嵌Tomcat或Jetty等Servlet容器；
（3）提供自动配置的“starter”项目对象模型（POMS）以简化Maven配置；
（4）尽可能自动配置Spring容器；
（5）提供准备好的特性，如指标、健康检查和外部化配置；
（6）绝对没有代码生成，不需要XML配置。
* 微服务（或微服务架构）是一种云原生架构方法，其中单个应用程序由许多松散耦合且可独立部署的较小组件或服务组成。这些服务通常有自己的堆栈，包括数据库和数据模型；
通过REST API，事件流和消息代理的组合相互通信；
* 它们是按业务能力组织的，分隔服务的线通常称为有界上下文。
* 尽管有关微服务的许多讨论都围绕体系结构定义和特征展开，但它们的价值可以通过相当简单的业务和组织收益更普遍地理解：
* 可以更轻松地更新代码。
* 团队可以为不同的组件使用不同的堆栈。
* 组件可以彼此独立地进行缩放，从而减少了因必须缩放整个应用程序而产生的浪费和成本，因为单个功能可能面临过多的负载。

# 快速入门

* 可以在[官网](https://start.spring.io/)直接配置下载入门项目。
* 也可以在idea中通过spring initializer快速创建springboot项目。
* ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210314111338.png)
* 默认项目结构如下图：
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210314111453.png)
  * 可以删除不必要的文件，如.mvn,.gitignore等。
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210314112222.png)
* 项目结构解释：
  * `SpringbootApplicaton.java`（项目名+Application.java）:是整个SpringBoot项目的主入口，不能删也不能改。
  * `application.properties`是SpringBoot的配置文件（一般会用.yml文件）。
  * test包下默认有一个测试类：`SpringbootApplicationTests.java`，即在主入口名后加上Tests。
  * 项目的代码**放在Application的同级目录中，在此例中，所有业务代码都应放在`com.zestaken.springboot`包下**。（可以在这个包下再建包）
  * 编写controller层代码，在页面上显示hello：
  ```java
  package com.zestaken.springboot.controller;


    import org.springframework.web.bind.annotation.RequestMapping;
    import org.springframework.web.bind.annotation.RestController;

    @RestController
    public class HelloController {

        @RequestMapping("/hello")
        public String hello() {
            return "hello springboot!";
        }
    }
    ```
    * 无需编写视图层，便能直接将结果显示到页面上：
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210314113132.png)
    ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20210314113033.png)
* pom.xml配置解释：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
<!--    有一个父项目 继承spring-boot-starter-parent的依赖管理，控制版本与打包等内容-->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.4.3</version>
        <relativePath/> <!-- lookup parent from repository -->
    </parent>
    <groupId>com.zestaken</groupId>
    <artifactId>springboot</artifactId>
    <version>0.0.1-SNAPSHOT</version>
    <name>springboot</name>
    <description>Demo project for Spring Boot</description>

<!--    java版本-->
    <properties>
        <java.version>1.8</java.version>
    </properties>


    <dependencies>

<!--        web依赖-->
<!--        所有springboot的依赖都是使用spring-boot-starter开头的-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>

<!--        单元测试依赖-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
<!--            打jar包的插件-->
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
```