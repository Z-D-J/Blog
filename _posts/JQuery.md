---
title: JQuery
date: 2021-01-21 17:35:45
tags:
---
# JQuery概念

* jQuery是一个快速、简洁的**JavaScript框架**，是继Prototype之后又一个优秀的JavaScript代码库（或JavaScript框架）。jQuery设计的宗旨是“write Less，Do More”，即倡导写更少的代码，做更多的事情。它封装JavaScript常用的功能代码，提供一种简便的JavaScript设计模式，优化**HTML文档操作、事件处理、动画设计和Ajax交互**。
* JavaScript框架：本质上就是一些**js文件**，这些文件中封装了js的原生代码。

# 快速入门

1. 下载JQuery
   1. 版本说明：
      1. 1.x：兼容ie678,使用最为广泛的，官方只做BUG维护，功能不再新增。因此一般项目来说，使用1.x版本就可以了，最终版本：1.12.4 (2016年5月20日)
      2. 2.x：不兼容ie678，很少有人使用，官方只做BUG维护，功能不再新增。如果不考虑兼容低版本的浏览器可以使用2.x，最终版本：2.2.4 (2016年5月20日)
      3. 3.x：不兼容ie678，只支持最新的浏览器。除非特殊要求，一般不会使用3.x版本的，很多老的jQuery插件不支持这个版本。目前该版本是官方主要更新维护的版本。最新版本：3.3.1（2018年1月20日） 
2. 导入JQuery的js文件：导入.min.js文件。
3. 使用

# JQuery对象和JS对象的区别与转换

* JQuery获取元素对象：`var $divs = $("div");`;
* JS获取元素对象：`var div2 = document.getElementsByTagName("div");`
* JQuery对象在操作时更加方便，但是**JQuery对象和JS对象的方法是不通用的**。
* JQuery对象和JS对象的互相转换：
  * JS-->JQ：`$(JS对象)`,如：`$(divs).html("修改html内容")`
  * JQ-->JS：`jq对象[索引]`或者`jq对象.get(索引)`,如：`$divs[1].innerHTML("修改HTML内容")`或者`$divs.get(0).innerHTML("修改HTML内容")`

# 选择器
