---
title: 会话技术-session
date: 2021-01-18 10:04:36
tags:
---

# session概述

* 概念：服务器端会话技术，在一次会话的多次请求间共享数据，将数据保存在服务器端的对象（HTTPSession)中。

# session快速入门

1. 获取HttpSession对象：`HttpSession session = request.getSession();`
2. 使用HttpSession对象：
   1. 获取属性：`Object getAttribute(String name)`
   2. 设置属性：`void setAttribute(String name, String value);`
   3. 删除属性：`void removeAttribute(Strin name)`

# session的基本原理

* 在一次会话范围内多次获取的Session对象是同一个Session对象。
* Session的实现是依赖于Cookie的：
  1.  在第一次请求创建了Session对象之后，服务器的`set-cookie`响应头之中会携带Session的id信息;
  2.  在客户端进行第二次请求时，会自动发送一个cookie头，在这个头中包含有`set-cookie`中携带回来的Session对象的Id信息;
  3.  服务器接受到Session的id信息后，或检查服务器中有无该session对象，如果有，则继续使用。 

