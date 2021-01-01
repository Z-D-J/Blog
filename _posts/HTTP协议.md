---
title: HTTP协议
date: 2021-01-01 17:40:01
tags:
---
# HTTP协议

## HTTP协议的概念

* **超文本传输协议（HTTP，HyperText Transfer Protocol)**是互联网上应用最为广泛的一种网络协议。所有的WWW文件都必须遵守这个标准。它是TCP/IP协议的一个应用层协议简单来说，HTTP协议就是**客户端和服务器交互**的一种通迅的格式。
* 特点：
  * 基于TCP/IP的高级协议;
  * 默认端口号：80;
  * 基于请求响应模型：**一次请求对应一次响应**
  * 无状态：每次**请求之间相互独立**，不能交互数据.

## HTTP1.0和HTTP1.1

* HTTP1.0协议中，客户端与web服务器建立连接后，只能获得**一个web资源**【短连接，获取资源后就断开连接】
* HTTP1.1协议，允许客户端与web服务器建立连接后，在一个连接上获取**多个web资源**【保持连接】

## HTTP请求

* 浏览器向服务器请求某个web资源时，称之为浏览器向服务器发送了一个http请求。一个完整http请求应该包含三个部分：
  1.  请求行【描述客户端的请求方式、请求的资源名称，以及使用的HTTP协议版本号】
  2. 多个消息头【描述客户端请求哪台主机，以及客户端的一些环境信息等】
  3. 一个空行

### 请求行

* 请求行：`GET /java.html HTTP/1.1`。请求行中的GET称之为请求方式，之后跟请求的路径，最后是请求协议版本。请求方式有：POST,GET,HEAD,OPTIONS,DELETE,TRACE,PUT。
* 常用的请求方式有：POST,GET
  * 一般来说，当我们点击超链接，通过地址栏访问都是get请求方式。通过表单提交的数据一般是post方式。
  * 可以简单理解GET方式用来**查询数据**,POST方式用来**提交数据**，get的提交速度比post**快**。
  * GET方式：在URL地址后附带的参数是有限制的，其**数据容量通常不能超过1K**。
  * POST方式：可以在请求的实体内容中向服务器**发送数据，传送的数据量无限制**。

### 请求头

* Accept: text/html,image/* 【浏览器告诉服务器，它支持的数据类型】
* Accept-Charset: ISO-8859-1 【浏览器告诉服务器，它支持哪种字符集】
* Accept-Encoding: gzip,compress 【浏览器告诉服务器，它支持的压缩格式】
* Accept-Language: en-us,zh-cn 【浏览器告诉服务器，它的语言环境】
* Host: www.it315.org:80【浏览器告诉服务器，它想访问哪台主机】
* If-Modified-Since: Tue, 11 Jul 2000 18:23:51 GMT【浏览器告诉服务器，缓存数据的时间】
* Referer: http://www.it315.org/index.jsp【浏览器告诉服务器，客户机是从那个页面来的---反盗链】
* 8.User-Agent: Mozilla/4.0 (compatible; MSIE 5.5; Windows NT 5.0)【浏览器告诉服务器，浏览器的内核是什么】
* Cookie【浏览器告诉服务器，带来的Cookie是什么】
* Connection: close/Keep-Alive 【浏览器告诉服务器，请求完后是断开链接还是保持链接】
* Date: Tue, 11 Jul 2000 18:23:51 GMT【浏览器告诉服务器，请求的时间】

## HTTP响应

* 一个HTTP响应代表着服务器向浏览器回送数据。一个完整的HTTP响应应该包含四个部分:
  1. 一个状态行【用于描述服务器对请求的处理结果。】
  2. 多个消息头【用于描述服务器的基本信息，以及数据的描述，服务器通过这些数据的描述信息，可以通知客户端如何处理等一会儿它回送的数据】
  3. 一个空行
  4. 实体内容【服务器向客户端回送的数据】

### 状态行

* 格式： HTTP版本号　状态码　原因叙述
* 状态行：HTTP/1.1 200 OK
* 状态码用于表示服务器对请求的处理结果，它是一个三位的十进制数。响应状态码分为5类:
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201010121055.png)

### 响应头

* Location: http://www.it315.org/index.jsp 【服务器告诉浏览器要跳转到哪个页面】
* Server:apache tomcat【服务器告诉浏览器，服务器的型号是什么】
* Content-Encoding: gzip 【服务器告诉浏览器数据压缩的格式】
* Content-Length: 80 【服务器告诉浏览器回送数据的长度】
* Content-Language: zh-cn 【服务器告诉浏览器，服务器的语言环境】
* Content-Type: text/html; charset=GB2312 【服务器告诉浏览器，回送数据的类型】
* Last-Modified: Tue, 11 Jul 2000 18:23:51 GMT【服务器告诉浏览器该资源上次更新时间】
* Refresh: 1;url=http://www.it315.org【服务器告诉浏览器要定时刷新】
* Content-Disposition: attachment; filename=aaa.zip【服务器告诉浏览器以下载方式打开数据】
* Transfer-Encoding: chunked 【服务器告诉浏览器数据以分块方式回送】
* Set-Cookie:SS=Q0=5Lb_nQ; path=/search【服务器告诉浏览器要保存Cookie】
* Expires: -1【服务器告诉浏览器不要设置缓存】
* Cache-Control: no-cache 【服务器告诉浏览器不要设置缓存】
* Pragma: no-cache 【服务器告诉浏览器不要设置缓存】
* Connection: close/Keep-Alive 【服务器告诉浏览器连接方式】
* Date: Tue, 11 Jul 2000 18:23:51 GMT【服务器告诉浏览器回送数据的时间】
