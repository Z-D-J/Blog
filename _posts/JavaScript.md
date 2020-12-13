---
title: JavaScript
date: 2020-12-13 21:02:41
tags:
---

# JavaScript概述

* 概念：一门客户端脚本语言
  * 运行在客户端浏览器中。每一个浏览器都有JavaScript的解析引擎。
  * **脚本语言**；不需要编译，直接就可以被浏览器解析执行。
* 功能：可以用来**增强用户与html页面的交互过程**，可以控制html元素，让页面有一些动态效果。
* JavaScript发展史：
  1. 1992年，Nombase公司，开发出第一门客户端脚本语言，专门用于表单的校验。命名为：c--，后来更名为ScriptEase。
  2. 1995年，Netbase（网景）公司，开发出一门客户端脚本语言：LiveScript；之后，该公司请来Sun公司的专家，修改LiveScript，命名为JavaScript。
  3. 1996年，微软抄袭了JavaScript开发出了JScript语言；
  4. 1997年，ECMA（欧洲计算机制造商协会），制定了ECMAScript，就是所有客户端脚本语言的标准。
* JavaScript=ECMAScript + JavaScript自己特有的东西(BOM+DOM)。

# ECMAScript

## 基本语法

### 与html结合的方式

1. 内部JS
   1. 定义一个`<script></script>`标签，标签体内容就是js代码。
   2. 示例：
```html
<script>
    alert("hello world");
</script>
```
2. 外部JS
   1. 定义一个`<script></script>`标签，通过src属性引入外部的js文件。
   2. 示例：
```html
<script src="js/a.js"></script>
```
* `<script>`标签可以写在html页面的任何位置，但是定义的位置的先后会**影响执行顺序**。
* 同一个html页面**可以定义多个`<script>`标签**。
