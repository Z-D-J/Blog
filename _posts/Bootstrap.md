---
title: Bootstrap
date: 2020-12-23 19:23:16
tags:
---

# Bootstrap概述

[官网](https://www.bootcss.com/)
* 基于HTML，CSS，JavaScript的前端开发框架。
  * **框架**：一个半成品软件，开发人员可以在框架基础上，再进行开发，简化编码。
* 优点：
  * 定义了很多**css样式**和**js插件**。
  * **响应式布局**：同一套页面可以兼容不同分辨率的设备。
* 快速入门：
  1. [下载Bootstrap](https://v3.bootcss.com/getting-started/#download)
  2. 在项目中将三个文件夹复制进来；
  3. 创建html文件，引入必要的资源文件（即下载的文件夹中的文件）
```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
    <title>Bootstrap 101 Template</title>

    <!-- Bootstrap -->
    <link href="css/bootstrap.min.css" rel="stylesheet">

    <!-- HTML5 shim 和 Respond.js 是为了让 IE8 支持 HTML5 元素和媒体查询（media queries）功能 -->
    <!-- 警告：通过 file:// 协议（就是直接将 html 页面拖拽到浏览器中）访问页面时 Respond.js 不起作用 -->
    <!--[if lt IE 9]>
    <script src="dist/html5shiv.min.js"></script>
    <script src="dest/respond.min.js"></script>
    <![endif]-->
</head>
<body>
<h1>你好，世界！</h1>

<!-- jQuery (Bootstrap 的所有 JavaScript 插件都依赖 jQuery，所以必须放在前边) -->
<script src="dist/jquery.min.js"></script>
<!-- 加载 Bootstrap 的所有 JavaScript 插件。你也可以根据需要只加载单个插件。 -->
<script src="dist/js/bootstrap.min.js"></script>
</body>
</html>
```

# 响应式布局

* 同一套页面可以兼容不同分辨率的设备。
* 实现：依赖于**栅格系统**。
  * 栅格系统：将一行平均分为**12个格子**，可以指定元素占几个格子。
* 步骤：
  * 定义容器。相当于table，通过**class**设置
    * 容器分类：
        1. container;
        2. container-fluid
  * 定义行。相当于tr ，通过class设置为row
  * 定义元素。指定该元素在不同的设备上，所占格子的数目。样式`col-设备代号-格子数目`
    * 设备代号：
        1. xs: 超小屏幕 手机(<768px)
        2. sm: 小屏幕 平板(>=768px)
        3. md: 中等屏幕 桌面显示器(>=992px)
        4. lg: 超大屏幕 大桌面显示器(>=1200px)
