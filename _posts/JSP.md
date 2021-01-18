---
title: JSP
date: 2021-01-13 23:48:38
tags:
---
# JSP概念

* JSP:Java Server Pages:java服务器端页面
* 一个特殊的页面，其中既**可以指定定义html标签，又可以定义java代码**，用于简化书写。

# JSP原理

* JSP文件本质上是一个Servlet类。
* 服务器请求JSP资源之后，服务器会先将JSP文件转换为一个java文件，然后再编译成.class文件，由.class文件提供服务。

# JSP脚本

* JSP脚本：JSP定义java代码的方式。
* `<% code %>`:定义的java代码，在servlce方法中。service方法中可以定义什么，该脚本中就可以定义什么。
* `<%! code %>`:定义的java代码,在JSP转换后的java类的成员位置。（定义该类的全局变量）
* `<%= code %>`:定义的java代码，会输出到页面上。输出语句中可以定义什么，该脚本中就可以定义什么。

# JSP的内置对象

* 在JSP页面中不需要获取和创建，可以直接使用的对象（其本质是JSP内部已经提前创建好了）
* JSP一共有9个内置对象：
  * request:
  * reponse:
  * out:字符输出流对象。可以将数据输出到页面上，和`response.getWriter()`类似。
    * `response.getWriter()`和`out.write()`的区别：
      * 在他tomcat服务器真正给客户端做出响应之前，会先找response的缓冲区数据，再找out缓冲区数据。
      * `response.getWriter()`数据输出永远在`out.write()`之前。
    
