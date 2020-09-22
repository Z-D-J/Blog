---
title: Maven
date: 2020-09-22 00:32:53
tags:
---

# maven是什么？

* maven是基于POM（project object model:项目对象模型）的软件项目管理工具。
* Maven 是一个项目管理工具，可以对 Java 项目进行构建、依赖管理。Maven 也可被用于构建和管理各种项目，例如 C#，Ruby，Scala 和其他语言编写的项目。

# maven的安装

* 参见：[菜鸟教程](https://www.runoob.com/maven/maven-setup.html)

# Maven POM

* **POM**( Project Object Model，项目对象模型 ) 是 Maven 工程的基本工作单元，是一个XML文件，包含了项目的基本信息，用于描述项目如何构建，声明项目依赖，等等。执行任务或目标时，Maven 会在当前目录中查找 POM。它读取 POM，获取所需的配置信息，然后执行目标。
* **父（Super）POM**是 Maven 默认的 POM。所有的 POM 都继承自一个父 POM（无论是否显式定义了这个父 POM）。父 POM 包含了一些可以被继承的默认设置。因此，当 Maven 发现需要下载 POM 中的 依赖时，它会到 Super POM 中配置的[默认仓库](http://repo1.maven.org/maven2) 去下载。
* POM的文件（xml）中的标签解读[菜鸟教程](https://www.runoob.com/maven/maven-pom.html)

# maven构建生命周期

* 生命周期概述：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20200922005205.jpg)

|阶段|处理|描述|
|-|-|-|
|验证 validate|	验证项目|	验证项目是否正确且所有必须信息是可用的|
|编译 compile|	执行编译	|源代码编译在此阶段完成|
|测试 Test|	测试|	使用适当的单元测试框架（例如JUnit）运行测试。|
|包装 package|	打包	|创建JAR/WAR包如在 pom.xml 中定义提及的包|
|检查 verify|	检查	|对集成测试的结果进行检查，以保证质量达标|
|安装 install|	安装|	安装打包的项目到本地仓库，以供其他项目使用|
|部署 deploy|	部署	|拷贝最终的工程包到远程仓库中，以共享给其他开发人员和工程|

# Maven构建配置文件