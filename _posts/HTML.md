---
title: HTML
date: 2020-12-08 09:05:40
tags:
---

# 概念

* 最基础的网页开发语言。
* HTML：Hyper Text Markup Language 超文本标记语言。
* 超文本：超文本是用超链接的方法，将不同空间的文字信息组织在一起的网状文本。
* 标记语言：
  * 由标签（<标签内容>）构成的语言，如html，xml
  * 标记语言不是编程语言，没有逻辑性。

# 快速入门

* html文档的后缀名：html或者htm
* 标签分为：
  * 围堵标签：有开始标签和结束标签。如：`<html></html>`
  * 自闭和标签：开始标签和结束标签在一起。如：`<br/>`
* 标签可以被嵌套：
  * 需要正确嵌套，不能你中有我，我中有你
  * 错误：`<a><b></a></b>`
  * 正确：`<a><b></b></a>`
* 在**开始标签**中可以定义属性。属性是由键值对构成，值需要用引号(单双都可，但是要统一)引起来。
* html的标签不区分大小写，但是建议使用小写。
```html
<html>

    <head>
            <title>title</title>
    </head>

    <body>
        <font color='red'>Hello world</font><br/>
        <font color='green'>Hello world</font>
    </body>
</html>
```
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201208092240.jpg)

# 标签

* [参考手册](https://www.w3school.com.cn/tags/index.asp)

## 文件标签

* 构成html最基本的标签。
* html:html文档的根标签
* head：头标签。用于指定html文档的一些属性，引入外部的资源。
* title:标题标签；
* body；体标签。
* <!DOCTYPE>:定义文档类型标签,html5中定义文档类型的方式。如：`<!DOCTYPE html>`
* 


