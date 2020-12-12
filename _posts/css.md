---
title: css
date: 2020-12-12 23:41:38
tags:
---

# css概述

* css概念：cascading style sheets,层叠样式表
  * 层叠：多个样式可以作用在一个html元素上，同时生效。
* 作用：
  * 功能较直接用html控制样式更加强大；
  * 将内容展示和样式控制分离
    * 降低耦合度，解耦
    * 让分工协作更容易
    * 提高开发效率
* css的使用：css与html结合的方式
  1. 内联方式：在**标签内**使用style属性指定css代码
     1. 如：`<div style="color:red;">hello css</div>`。
     2. 仅限于修改当前标签的内容样式，范围太小，且没有分离，一般不使用。
  2. 内部样式：在**head标签内**，定义style标签，style标签的标签体内容就是css代码
     1. 仅限于修改当前页面的内容
     2. 如：
   ```html
   <style>
    div{
        color:red;
    }
    </style>
    ```
  3. 外部样式：
    1.  定义css资源文件
    2. 在**head标签**内，定义**link标签**，引入外部的资源文件。  
    3. 如：
```html
<link rel="stylesheet" href="css/a.css">

<!--也可以通过下面方式引入css，但是不常用-->
<style>
    @import "css/a.css";
</style>
```

# css基本语法

* 格式：
```
选择器 ｛
    属性名1：属性值1；
    属性名2：属性值2；
    ...
｝
```
* 选择器：筛选具有相似特征的元素
* 每一对属性需要**使用;隔开**，最后一对属性可以不加。
