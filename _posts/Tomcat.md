---
title: Tomcat
date: 2020-10-08 16:42:03
tags:
---

# Tomcat简介

* Tomcat 服务器是一个免费的开放源代码的Web 应用服务器，属于轻量级应用[服务器](https://baike.baidu.com/item/服务器)，在中小型系统和并发访问用户不是很多的场合下被普遍使用，是开发和调试JSP 程序的首选。Tomcat是一个使别人能够访问我写的页面的一个程序。
* Tomcat与servlet以及数据库的关系：![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201008164643.png)

# Tomcat的配置

* Tomcat需要jdk的支持，需要先在电脑上装上jdk，Tomcat会在环境变量中去寻找jdk的支持。
* 去[官网](https://tomcat.apache.org)下载Windows系统的tomcat安装器：![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201008165449.jpg)
* 找到Tomcat安装目录的bin目录中的startup.bat文件，打开得到如下界面：![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201008170319.jpg)

* 之后再浏览器地址栏输入http://localhost:8080成功显示出如下界面，则证明Tomcat的配置成功了。![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201008170513.jpg)

# Tomcat的基础知识

## 链接URL简介

![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201008173307.png)

## Tomcat的目录结构

![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201008173457.png)

* conf文件：	
	* `server.xml`该文件用于配置server相关的信息，比如tomcat启动的端口号，配置主机(Host)
	* `web.xml`文件配置与web应用（web应用相当于一个web站点）
	* `tomcat-user.xml`配置用户名密码和相关权限.
* work文件：
  * work工作目录：该目录用于存放**jsp被访问后生成对应的server文件和.class文件**
* webapps目录：
  * 