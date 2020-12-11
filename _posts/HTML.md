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
* HTML 文档描述网页,HTML 文档包含 HTML 标签和纯文本,HTML 文档也被称为网页


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
* html的标签不区分大小写，但是建议使用小写
* 。
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
* html:html文档的根标签,<html> 与 </html> 之间的文本描述网页
* head：头标签。用于指定html文档的一些属性，引入外部的资源。
* title:标题标签；
* body；体标签，放网页显示内容.`<body>` 与 `</body>` 之间的文本是**可见**的页面内容。
* <!DOCTYPE>:定义文档类型标签,html5中定义文档类型的方式。如：`<!DOCTYPE html>`

## 文本标签

* 注释：`<!--注释内容 --!>`
* 标题：`<h1>标题内容</h1>`共有6级标题。
* 定义段落：`<p>这是段落内容</p>`,p 元素会自动在其前后创建一些空白。浏览器会自动添加这些空间，您也可以在样式表中规定。
* 换行：`<br>`，如：`白日依山尽，<br>黄河入海流`,注意这是一个**自闭合标签**无需结束标签。（`<br/>`具有相同的效果）。
* 定义水平线：`<hr>`或者`<hr/>`可以定义一条水平线。
* 粗体：`<b>需要粗体内容</b>`。
* 斜体：`<i>需要斜体的内容</i>`.
* 类似打字机或者等宽的文本效果：`<tt>需要等宽显示的内容<tt>`
* 呈现大号字体效果:`<big>需要显示大号字体的内容</big>`
* 呈现小号字体效果:`<small>需要显示小号字体的内容<small>`
* 规定文本的字体、字体尺寸、字体颜色:`<font color="red", size="5",face="楷体"> 我是红色</font>`,face是指的字体。**已经不建议使用，改变样式现在用css**
* 文本居中：`<center>需要居中的内容</center>`,居中是相对于父元素来说的。示例：
```html
<center>
<font color="red", size="5",face="楷体"> 我是红色</font>
</center>
```
* 属性：
  * color:颜色：
    * 英文单词：red,green,blue等
    * rgb(值1，值2，值3)；rgb分别是红，绿，蓝三种颜色的占比。值的范围：0~255（不常用）
    * `#值1值2值3`:值的范围：00~FF之间。效果也是通过三种颜色的占比来配色。如：`#FF00FF`。
  * width:
    * 数值:width='20',数值的单位，默认是像素px(像素)；
    * 数值%：width='50%',相对于父元素的占比。
  * align:对齐方式
    * center:居中
    * left：左对齐
    * right：右对齐

## 图片标签

* `<img />`:图片标签是自闭合标签
* 属性：src
  * src后输入图片的位置；
  * 相对路径：
    * `./...`代表当前目录；如：`./image/1.jpg`
    * `../...`代表上一级目录：如：`../image/2.jpg`
  * 绝对路径也可以使用
  * 直接使用链接也可以
* 示例：
```html
<img src = "https://gitee.com/zhangjie0524/picgo/raw/master/img/20201208092240.jpg">
```

## 列表标签

* 有序列表
  * ol:定义有序列表
  * li：定义列表的项目
```html
<ol>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol>
```
效果：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201211102931.jpg)
* 无序列表：
  * ul:定义无序列表
  * li：定义列表的项目
  * 示例：
```html
<ul>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ul>
```
效果：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201211103137.jpg)

## 链接标签

* `<a></a>`:定义超链接
* 属性：
  * href：指定访问资源的url
    * 既可以是网页链接
    * 也可以是本地的资源，如：`./5_列表标签.html`。
  * target:
    * "_self",在当前页面打开链接的网页
    * "_blank":在一个空白标签页打开链接的网页
* 示例：
```html
<a href = "https://gitee.com/zhangjie0524/picgo/raw/master/img/20201211103137.jpg" target = "_blank">我是超链接</a>
```

## div和span




