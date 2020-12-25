---
title: XML
date: 2020-12-25 09:31:06
tags:
---

# XML概述

[参考手册](https://www.w3school.com.cn/xml/index.asp)
* 概念：Extensible Markup Language 可扩展标记语言
  * 可扩展：标签都是自定义的。
* 功能：
  * 存储数据
    * 作为配置文件
    * 在网络中传输
* XML与HTML：
  * 都是w3c（万维网联盟）的产物
  * xml的标签都是自定义的，html的标签是预定义的；
  * xml的语法严格，html的语法松散；
  * xml是存储数据的，html是展示数据的。

# 基本语法 

* xml文档的后缀名为`xml`;
* xml文档的**第一行**定义为**文档声明**。
* xml中**有且仅有一个根标签**。
* 属性值必须用引号（单双均可）引起来。
* 标签必须正确关闭（要么是围堵标签，要么是自闭和标签）;
* xml标签名称**区分大小写**。

# 组成部分

1. 文档声明
   1. 格式：`<?xml 属性列表 ?>`
   2. 属性列表：
      1. version:版本号，**必须的属性**;
      2. encoding:编码方式。告知解析引擎当前文档使用的字符集，默认值：ISO-8859-1
      3. standalone:是否独立，一般不会用
        * yes：不依赖于其他文件
        * no：依赖其他文件
2. 指令
   1. 示例：`<?xml-stylesheet type="text/css" href="a.css">`
3. 标签
   * 名称可以含字母、数字以及其他的字符
   * 名称不能以数字或者标点符号开始
   * 名称不能以字符 “xml”（或者 XML、Xml）开始
   * 名称不能包含空格
4. 属性
   * id属性值唯一
5. 文本
    * **CDATA**区：在该区域中的数据会被原样展示
      * 格式：`<![CDATA[需要展示的数据]]>`

# 约束

* 约束：规定XML文档的书写规则
* XML与约束之间的关系图：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201225180146.png)
* 分类：
  * DTD:简单的约束技术
  * Schema:复杂的约束技术
* DTD：
  * [参考资料](https://www.w3school.com.cn/dtd/dtd_intro.asp)
  * 约束文件名的后缀为`.dtd`
  * 引入dtd文档到xml文档中，之后如果xml的书写不满足dtd文档的规范，则会报错。
    * 内部dtd：将约束规则定义在xml文档中
      * 样式；`<!DOCTYPE 根标签名 [dtd约束规则内容]>`
    * 外部dtd：将约束的规则定义在外部的dtd文件中
      * 本地：`<!DOCTYPE 根标签名 SYSTEM "dtd文件在本机的位置（相对路径）">`
      * 网络:`<!DOCTYPE 根标签名 PUBLIC "dtd在本地的文件名""dtd文件在网络的位置（URL）">`
  * 无法规定标签内的内容
* Schema:
  * [参考资料](https://www.w3school.com.cn/schema/index.asp)
  * 是DTD的替代者，可以规定标签体内的内容格式。
  * Schema文档的后缀名为`.xsd`
  * 在xml文档中引入Schema文档：
    1. 填写xml文档的的**根元素**
    2. 引入xsi前缀：`xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"`,后面的内容又很多种选择，可以根据ide的提示内容来选择。
    3. 引入xsd文件的命名空间：`xsi:schemaLocation="http://www.w3school.com.cn note.xsd"`前面的内容可以自定义，后面的内容是xsd文件名
    4. 为每一个xsd约束声明一个前缀，作为标识：`xmlns="http://www.w3school.com.cn`或者`xmlns:a="http://www.w3school2.com.cn`,如果没有指定前缀的话则默认为空前缀。
    5. 引入的每个xsd文件对应一个前缀，该xsd文件内的标签在使用时必须带上该xsd文件的前缀，（空前缀除外）。如：`<students></students>`和`<a:students></a:students>`

# 解析

