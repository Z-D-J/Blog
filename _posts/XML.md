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

* 对xml文档的操作：
  1.  解析（读取）：将文档中的数据**读取到内存中**。
  2.  写入：将内存中的数据保存到xml文档中，持久化的存储。
* 解析xml的方式：
  1.  DOM：将标记语言文档**一次性**加载进内存，在内存中形成一颗DOM树。
      1.  优点：操作方便，可以对文档进行**CRUD**的所有操作。
      2.  缺点:因为一次性读取，且DOM树占内存，所以十分消耗内存。
  2. SAX：**逐行**读取，基于事件驱动的。
     1. 优点：不占内存
     2. 缺点：**只能读取**，不能CRUD。
* XML常见的解析器：基于不同的解析的方式写出来的**工具包**。
  * JAXP：sun公司提供的解析器，支持DOM和SAX思想，不常用。
  * DOM4J:非常优秀的基于DOM思想的解析器。
  * Jsoup:jsoup 是一款Java 的HTML解析器，可直接解析某个URL地址、HTML文本内容。它提供了一套非常省力的API，可通过DOM，CSS以及类似于jQuery的操作方法来取出和操作数据。也可以用来解析XML。
  * PULL：Android操作系统内置的解析器，基于SAX思想。

# Jsoup


## 快速入门

* 步骤：
  1. 导入jar包
     1. 在[官网](https://jsoup.org/download)下载jar包
  2. 获取Document对象
     1. 获取对应xml的路径：`String path = JsoupDemo1.class.getClassLoader().getResource("student.xml").getPath();`即：`String path = 类名.class.getClassLoader().getResource("xml文档名").getPath();`
     2. 解析xml文档，加载文档进内存，获取DOM树（对应Document对象）：`Document document = Jsoup.parse(new File(path),"utf-8");` 即：`Document document = Jsoup.parse(new File(path),"和xml文档一致得字符集");`
  3. 获取对应的标签（Element对象）
  4. 获取数据

     1. 获取元素对象：`Elements elements = document.getElementsByTag("name");`即：`Elements elements = Document对象名.getElementsByTag("标签名");`
     2. Elements是一个类似集合的对象，它里面会依次存好符合条件得所有元素对象。
  4. 获取数据

## 对象的使用

* Jsoup:工具类，可以解析html或xml文档，返回Document对象
  * parse方法：解析html或者xml文档，返回Document对象
    * `parse(File in ,String charseName)`:解析本地的xml或html文件
    * `parse(String html)`:解析xml或者html字符串；
    * `parse(URL url, int timeoutMills);`:通过网络路径获取指定的html或xml的文档对象。
      * timeoutMills：指的是超时时间，如果超过这个时间还没有响应的话则认为获取失败。
* Document:文档对象，代表内存中的DOM树
* Elements：元素ELement对象的集合，可以当作`ArrayList<Element>`来使用
* Element：元素对象
* Node：节点对象。

