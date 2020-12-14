---
title: JavaScript
date: 2020-12-13 21:02:41
tags:
---

# JavaScript概述

[参考资料](https://www.w3school.com.cn/js/index.asp)

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

## 注释

* 单行注释：//注释内容
* 多行注释：/* 注释内容 */

## 数据类型

* 原始数据类型（类似java中的基本数据类型）
  * number:数字。
    * 整数
    * 小数
    * NaN(not a number 一个不是数字的数字类型)
  * string:字符串
    * "abc","a",'a'都是字符串，没有字符类型。
  * null:一个对象为空的占位符。
  * undefined:未定义。如果一个变量没有给初始化值，则会被默认赋值为undefined。
  * boolean：布尔值类型，值为true或者false。
* 引用数据类型：对象。

## 变量

* 变量定义：一小块存储数据的内存空间
* java是强类型语言，JavaScript是弱类型语言
  * 强类型：在开辟变量存储空间时，定义了空间将来存储的数据类型。**只能存储固定类型的数据**。
  * 弱类型：在开辟变量存储空间时，不定义空间将来的存储数据类型，**可以存放任意类型的数据**。
* 语法:`var 变量名;`或者`var 变量名 = 初始化值;`
* 查看数据类型：`typeof(变量名);`,会返回变量的类型。
* 输出数据到页面中`document.write(输出的数据);`,如：`document.write(a+"我是a"+"<br>");`

## 运算符

* 一元运算符：
  * `++`:自增
  * `--`:自减（同java一样，也有放在前后的问题）
  * `+/-`:正负号。
* 算数运算符：
  * `+`:加法
  * `-`:减法
  * `*`:乘法
  * `/`:除法，与java不同的是，除法的结果**可以为小数**.
  * `%`:取余运算。
* 赋值运算符：
  * `=`；赋值
  * `+=`
  * `-=`:与java相同。
* 比较运算符：
  * 类型相同，直接比较，如果是字符串则按照字典顺序**按位逐个比较**，直到得出大小。
  * 类型不同，**转换后再相比**。
  * `>,<，>=，<=`:大于、小于,大于等于，小于等于
  * `===`:比较之前先判断类型，如果**类型不相同则直接返回false**。
* 逻辑运算符：
  * `&&`:与，有短路效果(如果左边能够确定表达式的值，那么右边就不会再运算)
  * `||`:或，也有短路效果。
  * `!`:非，该运算符要求变量类型是boolean。
* 三元运算符：
* 在JavaScript中如果运算数不是运算符所要求的类型，那么js引擎会自动地将运算数进行类型转换。
  * 其它类型转number：
    * String转number：会按照字面值转换，如果**字面值不是数字，那么转换为NaN**.（NaN与任何数运算的结果还是NaN）
    * boolean转number：true转为1，false转为0。
    * 其它类型转换为number就是**NaN**。
  * 其它类型转boolean：
    * number转为boolean：**0或NaN**为false，其它为true。
    * string转为boolean：**空字符串**为false，其它都为true。空字符串：`string str="";`
    * null和undefined转为boolean：**都是false**。
