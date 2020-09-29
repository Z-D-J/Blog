---
title: Maven
date: 2020-09-22 00:32:53
tags:
---

# maven是什么？

* maven是基于POM（project object model:项目对象模型）的软件项目管理工具。
* Maven 是一个项目管理工具，可以对 Java 项目进行构建、依赖管理。Maven 也可被用于构建和管理各种项目，例如 C#，Ruby，Scala 和其他语言编写的项目。
)
* Maven 可以统一**管理所有的依赖 jar**，甚至是不同的版本。程序员也可以动态地将自己写好的模块打包成 jar 包让它管理。需要的时候，可以直接通过简单的描述文件告诉 Maven，它会自动帮助程序员找出来，集成到项目中。并且它提供了中央仓库，能帮我们自动下载构件。
* maven可以进行对指定目录下的代码进行单元测试，检测代码质量。


# maven的安装

* 参见：[菜鸟教程](https://www.runoob.com/maven/maven-setup.html

# Maven POM

* **POM**( Project Object Model，项目对象模型 ) 是 Maven 工程的基本工作单元，是一个XML文件，包含了项目的基本信息，用于描述项目如何构建，声明项目依赖，等等。执行任务或目标时，Maven 会在当前目录中查找 POM。它读取 POM，获取所需的配置信息，然后执行目标。
* **父（Super）POM**是 Maven 默认的 POM。所有的 POM 都继承自一个父 POM（无论是否显式定义了这个父 POM）。父 POM 包含了一些可以被继承的默认设置。因此，当 Maven 发现需要下载 POM 中的 依赖时，它会到 Super POM 中配置的[默认仓库](http://repo1.maven.org/maven2) 去下载。
* POM的文件（xml）中的标签解读[菜鸟教程](https://www.runoob.com/maven/maven-pom.html)

# maven构建生命周期

* 生命周期概述：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20200922005205.jpg)

* 默认生命周期：


|阶段|处理|命令｜描述|
|-|-|-|-|
|验证 validate|	验证项目||	验证项目是否正确且所有必须信息是可用的|
|编译 compile|	执行编译	|mvn compile|源代码编译在此阶段完成|
|测试 Test|	测试|mvn test|	使用适当的单元测试框架（例如JUnit）运行测试。|
|包装 package|	打包	|mvn package|创建JAR/WAR包如在 pom.xml 中定义提及的包|
|检查 verify|	检查	||对集成测试的结果进行检查，以保证质量达标|
|安装 install|	安装|	mvn install|安装打包的项目到本地仓库，以供其他项目使用|
|部署 deploy|	部署	|mvn deploy|拷贝最终的工程包到远程仓库中，以共享给其他开发人员和工程|

* 清理生命周期；清除项目编译信息：mvn clean

# Maven构建配置文件

# Maven的仓库

* Maven 仓库能帮助我们管理构件（主要是JAR），它就是放置所有JAR文件（WAR，ZIP，POM等等）的地方。即jar不是放在项目中，而是放在仓库中，实际使用的时候，maven通过jar包的坐标在**仓库**中定位jar包。
* Maven 仓库有三种类型：
  1. 本地（local）
  2. 中央（central）
  3. 远程（remote）
* 本地仓库：
    * 运行 Maven 的时候，Maven 所需要的任何构件都是直接从本地仓库获取的。如果本地仓库没有，它会首先尝试从远程仓库下载构件至本地仓库，然后再使用本地仓库的构件。 
    *Maven 本地仓库默认被创建在 %USER_HOME% 目录下。要修改默认位置，在 %M2_HOME%\conf 目录中的 Maven 的 settings.xml 文件中定义另一个路径。当你运行 Maven 命令，Maven 将下载依赖的文件到你指定的路径中。
    ```xml
    <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 
    http://maven.apache.org/xsd/settings-1.0.0.xsd">
        <localRepository>C:/MyLocalRepository</localRepository>
    </settings>
    ```
* 中央仓库：
  * 这个仓库由 Maven 社区管理。
  * 不需要配置。
  * 需要通过网络才能访问。
  * 要浏览中央仓库的内容，maven 社区提供了一个 URL：http://search.maven.org/#browse。使用这个仓库，开发人员可以搜索所有可以获取的代码库。
* 远程仓库：
    * 如果 Maven 在中央仓库中也找不到依赖的文件，它会停止构建过程并输出错误信息到控制台。为避免这种情况，Maven 提供了远程仓库的概念，它是开发人员自己定制仓库，包含了所需要的代码库或者其他工程中用到的 jar 文件。
* 依赖的搜索顺序：
    1. 步骤 1 － 在本地仓库中搜索，如果找不到，执行步骤 2，如果找到了则执行其他操作。
    2. 步骤 2 － 在中央仓库中搜索，如果找不到，并且有一个或多个远程仓库已经设置，则执行步骤 4，如果找到了则下载到本地仓库中以备将来引用。
    3. 步骤 3 － 如果远程仓库没有被设置，Maven 将简单的停滞处理并抛出错误（无法找到依赖的文件）。
    4. 步骤 4 － 在一个或多个远程仓库中搜索依赖的文件，如果找到则下载到本地仓库以备将来引用，否则 Maven 将停止处理并抛出错误（无法找到依赖的文件）。

# Maven插件

* 每个生命周期中都包含着一系列的阶段(phase)。这些 phase 就相当于 Maven 提供的统一的接口，然后这些 phase 的实现由 Maven 的插件来完成。
* Maven 生命周期的每一个阶段的具体实现都是由 Maven 插件实现的。Maven 实际上是一个依赖插件执行的框架，每个任务实际上是由插件完成。Maven 插件通常被用来：1.创建 jar 文件 2.创建 war 文件 3.编译代码文件 4.代码单元测试 5.创建工程文档 6.创建工程报告。
* 插件的执行：`<code>mvn [plugin-name]:[goal-name]</code>`
* 常用插件：

|插件|描述|
|-|-|
|clean|	构建之后清理目标文件。删除目标目录。|
|compiler	|编译 Java 源文件。|
|surefile|	运行 JUnit 单元测试。创建测试报告。|
|jar	|从当前工程中构建 JAR 文件。|
|war	|从当前工程中构建 WAR 文件。|
|javadoc	|为工程生成 Javadoc。|
|antrun	|从构建过程的任意一个阶段中运行一个 ant 任务的集合。|

* 插件是在 pom.xml 中使用 plugins 元素定义的。每个插件可以有多个目标。

# maven的目录结构

* 核心代码部分；
* 配置文件部分：jar包之外的部分。
* 测试代码部分；
* 测试配置文件部分。
* maven标准目录结构：
  * src/main/java:核心代码部分
  * src/main/resources:配置文件部分
  * src/test/java：测试代码部分
  * src/test/resources:测试配置文件
  * src/main/webapp:页面资源，js，css，图片等。

# pom.xml

* 项目对象模型：
  * 项目自身信息
  * 项目运行所依赖的jar包信息
  * 项目运行环境信息，比如jdk信息。
* 依赖管理模型：（dependency）
  * 管理jar包
* 插件（plugins）
  * 生命周期的每一个过程都对应底层的一个插件




