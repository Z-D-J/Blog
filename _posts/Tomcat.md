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



# webapps目录：

* **在webapps中建立了web1目录**，下面放置我们的html文件，jsp文件，图片等等，**则web1就被当做web应用管理起来**。示例：![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201009103542.jpg)

  ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201009103533.jpg)

  * 注意路径是严格大小写的，路径出错是无法显示的。

* web站点的目录规范：
  ![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201009104107.png)
  * 作用：我有多个html文件，想把其中的一个html文件作为我web站点的首页。如果没有WEB-INF目录下的web.xml文件支持，是无法解决我的需求的。这个规范是约定熟成的。

  * web.xml使helloworld2.html做首页示例：

    * 新建一个WEB-INF目录![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201009151532.jpg)
    * 在WEB-INF目录下创建一个web.xml
    * web.xml我们不可能会写，所以可以**在webapps目录下其他的站点中抄一份过来**【复制ROOT/WEB-INF/web.xml的文件到自己的站点中】
    * 在web.xml中添加以下代码

    ```xml
          <welcome-file-list>
                <welcome-file>helloworld2.html</welcome-file>
          </welcome-file-list>
    ```

    * 最终的web.xml如图：![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201009151441.jpg)
    * 在浏览器输入`localhost:8080/web1/`得：![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201009151224.jpg)
      * 因为已经规定了首页为helloworld2.html所以无需指明具体的html文件。



# 配置虚拟目录

* 虚拟目录的作用：
  * 如果把所有web站点的目录都放在webapps下，可能导致**磁盘空间不够用**，也**不利于对web站点目录的管理**【如果存在非常多的web站点目录】
  * 把**web站点的目录分散到其他磁盘管理就需要配置虚拟目录【默认情况下，只有webapps下的目录才能被Tomcat自动管理成一个web站点】**
  * 把web应用所在目录交给web服务器管理，这个过程称之为虚拟目录的映射。
* 虚拟目录的配置方法一：
  * 在其他地方创建一个web站点目录，并创建WEB-INF目录和一个html文件。![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201009152314.jpg)
  * 找到Tomcat目录下/conf/server.xml文件
  * 在server.xml中的<Host>节点下添加如下代码。**path表示的是访问时输入的web项目名，docBase表示的是站点目录的绝对路径**` <Context path="/web" docBase="C:\03Temporary\web"/>`
  * 最后访问配置好的站点:`localhost:8080/web/helloworld.html`
* 虚拟目录的配置方法二：
  * 