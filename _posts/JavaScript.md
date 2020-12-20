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

### 注释

* 单行注释：//注释内容
* 多行注释：/* 注释内容 */

### 数据类型

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

### 变量

* 变量定义：一小块存储数据的内存空间
* java是强类型语言，JavaScript是弱类型语言
  * 强类型：在开辟变量存储空间时，定义了空间将来存储的数据类型。**只能存储固定类型的数据**。
  * 弱类型：在开辟变量存储空间时，不定义空间将来的存储数据类型，**可以存放任意类型的数据**。
* 语法:`var 变量名;`或者`var 变量名 = 初始化值;`
* 查看数据类型：`typeof(变量名);`,会返回变量的类型。
* 输出数据到页面中`document.write(输出的数据);`,如：`document.write(a+"我是a"+"<br>");`

### 运算符

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
  * `?:`:
    * 语法：`表达式?值1:值2`
    * 判断表达式的值，如果是true则取值1，否则取值2；
    * 示例：`a > b ? 1:0;`
* 在JavaScript中如果运算数不是运算符所要求的类型，那么js引擎会自动地将运算数进行类型转换。
  * 其它类型转number：
    * String转number：会按照字面值转换，如果**字面值不是数字，那么转换为NaN**.（NaN与任何数运算的结果还是NaN）
    * boolean转number：true转为1，false转为0。
    * 其它类型转换为number就是**NaN**。
  * 其它类型转boolean：
    * number转为boolean：**0或NaN**为false，其它为true。
    * string转为boolean：**空字符串**为false，其它都为true。空字符串：`string str="";`
    * null和undefined转为boolean：**都是false**。

### 特殊语法

* 语句以分号结尾，如果一行只有一条语句，则分号可以省略（但是一般不建议）；
* 变量的定义使用var关键字，也可以不使用：（不建议使用）
  * 使用var定义的局部变量
  * 不使用var定义的是全局变量

### 流程控制语句

* `if...else`:与java中相同
* `switch`:
  * 在java中，switch可以接收的数据类型：byte，int,short ,char ,枚举(1.5之后)，string(1.7之后)；
  * 在JavaScript中，switch可以接收任意类型的变量。
```javascript

var a = "hello";
switch(a) {
  case 1:
      alert("number");
      break;
  case "hello":
      alert("string");
      break;
  case undefined:
      alert("undefined");
      break;
}
```
* `while`:与java一样。
* `for`:与java一样
* `do...while`:与java一样。

### 示例：99乘法表

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>99乘法表</title>

    <style>
        td{
            border: 1px solid ;
        }
    </style>
    
    <script>
        document.write("<table align='center'>"); //在JavaScript的字符串中嵌套html的语句中如果含有双引号，则全部使用单引号，防止和字符串的双引号起冲突

        for(var i = 1; i <= 9; i++) {
            document.write("<tr>");
            for(var j = 1; j <= i; j++) {
                document.write("<td>");
                document.write(i + "*" + j + "=" + i * j + "&nbsp;&nbsp;&nbsp;&nbsp;");//&nbsp
                document.write("</td>");
            }
            document.write("</tr>");
        }

        document.write("</table>");
    </script>
</head>
<body>

</body>
</html>
```
* 效果：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201214170043.jpg)
* 在html代码中，使用转义字符`&nbsp`表示1个空格,在html代码中每输入一个转义字符`&nbsp`就表示一个空格，输入十个`&nbsp`，页面中就显示10个空格位置。而在html代码中输入空格，**不管输入多少个空格，最终在页面中显示的空格位置只有一个**。
* 在JavaScript的字符串中嵌套html的语句中如果含有双引号，则全部**使用单引号**，防止和字符串的双引号起冲突。

## 基本对象

### Function对象

* Function对象：函数（方法）对象
* 创建：
  1. 不常用：`var fun = new Function(形式参数列表，方法体);`
  2. 常用1：`function 函数名(形式参数列表) {方法体}`示例：
```javascript
function fun1(a,b) {
  alert(a + b);
}
```
  3. 常用2：`var 方法名 = function(形式参数列表) {方法体}`示例：
```javascript 
var fun2 = function(a, b) {
  alert(a + b);
}
```
* 特点：
  * 方法定义时，**不用写形参的类型**，也不用写**返回值类型**。
  * **方法是一个对象**，如果定义名称相同的方法，会覆盖而不会报错。
  * 在js中，方法的调用只与方法名有关，和**形参列表无关**（即使传入的参数不符合形参列表，也没有问题，如果传少了，则默认传了undefined，如果传多了，则不管多的）。
  * 在方法声明中有一个隐藏的内置对象（数组对象）`arguments`,封装了所有传进函数的**参数**。
* 属性：
  * length；方法对象中**形参**的个数。
* 调用：
  * `方法名(实际参数列表);`

### Array对象

* Array:数组对象
* 创建：
  1. `var arr = new Array(元素列表);`
  2. `var arr = new Array(默认长度);`
  3. `var arr = [元素列表];`
  4. `var arr = new Array();`
* 特点：
  * JS中，数组中元素类型是可变的，如：`var arr = [1, "hello",true];`
  * JS中，数组的长度是可变的，定义时写的只是默认的长度。
* 方法；
  * `join(参数)`:将数组中的元素按照**指定的分隔符（参数）**拼接为字符串。直接打印数组，会默认按照`,`为分隔符的方式拼接字符为字符串:`document.write(arr);`或者没有给join指定参数也是默认为`,`。返回一个字符串。
    * 示例：`document.write(arr.join("--"));`
  * `push();`:向数组末尾添加一个或者更多元素，并返回**新的长度**。

### Boolean对象

* 基本类型boolean的包装类。

### Date对象

* Date：日期对象；
* 创建：
  1. `var date = new Date();`
* 方法：
  * `toLocalString();`:返回当前Date对象对应的时间本地字符串格式。
  * `getTime();`:获取毫秒值，返回当前日期对象描述的时间到1970年1月1日零点的毫秒值差。

### Math对象

* Math:数学对象
* 创建：
  1. 不用创建，直接使用，`Math.方法名();`
* 方法：
  * `random();`:返回0~1之间的随机数（包含0，不包含1）
  * `round(x);`:对数字进行四舍五入取整；
  * `ceil(x)`:对数进行上舍入取整；
  * `floor(x);`对数进行下舍入取整。

### RegExp对象

* 正则表达式对象；
* 正则表达式：定义字符串的组成规则；
  * 单个字符：`[]`
    * 如:`[a]`:该字符为需要为a；`[ab]`:该字符可以为a或者b；`[a-zA-Z0-9]`:该字符可以为大写字母或者小写字母或者0到9的数字。
    * **特殊符号**代表特殊含义的单个字符
      * `\d`:单个数字字符`[0-9]`
      * `\w`:单个字符：`[a-zA-Z0-9]`;
  * 量词符号：
    * `?`:出现0次或者1次；
    * `*`:表示0次或者多次；
    * `+`:出现1次或者多次；
    * `{m,n}`:表示`m<=次数 <=n`
      * m如果缺省，`{:n}`表示最多n次；
      * n如果缺省：`{m:}`表示最少m次。
  * 开始结束符号：
    * `^`:开始
    * `$`:结束
* 创建：
  1. `var reg = new RegExp("正则表达式");`
     1. 该种类型要注意字符串内部的特殊符号需要**转义**
     2. 如：`\`在字符串内需要表达为`\\`,所以：`var reg - new  RegExp("^\\w(6,12)$);`
  2. `var reg = /正则表达式/;`
  3. 示例：`var reg = /^\w(6,12)$/;`
* 方法：
  * `test(参数);`:验证指定的字符串是否符合正则定义的规范,返回true或者false。
  * 示例：
```javascript
var reg = /^\w(6,13)$/;
var username = "zhanngsanlijskjdlfkajl";
var flag = reg.test(username);
```

### Global对象

* 是一个**全局对象**，这个对象中封装的方法**不需要任何对象**就可以直接调用，如：`方法名();`
* 方法：
  * URL码：因为网络协议中不支持中文，所以需要将汉字转为URL码来传输。
  * `encodeURI()`:url编码
  * `decodeURI()`:URL解码，与encodeURI配套使用。
  * `encodeURICompoent()`:也是进行URL编码，但是编码的字符更多（对有些符号也会进行编码）。
  * `decodeURICompoent()`:也是进行URL解码，配套使用。
  * 示例：
```javascript
var str = "张杰";
var encode = encodeURI(str);
```
  * `parseInt()`:将字符串转为数字
    * 逐一判断每一个字符是否为数字，直到不是数字为止，将前边的数字部分转为number。
```javascript
var str = "123abc";
var number = paseInt(str);//结果是123
```
  * `isNaN()`:判断一个值是否为NaN
    * NaN六亲不认，连自己都不认，NaN参与的所有`==`比较，结果都是false。
    * 因为`NaN == NaN`结果也是false，所以设计这个方法来判断一个值是否为NaN。
  * `eval()`:将Javascript的字符串转换为脚本代码来执行。示例：
```javascript
var jscode="alert(123)";
eval(jscode);//等效于直接写alert（123）；
```

# BOM

* 概念：Browser Object Model 浏览器对象模型
* 功能：将浏览器各个组成部分封装成对象
* 组成：
  * **Window**：浏览器窗口对象
  * **History**:历史记录对象
  * **Location**：地址栏对象
  * Screen：显示器屏幕对象
  * Navigator:浏览器对象

## Window对象

* window**不需要创建**，可以直接使用。也可以不用对象，直接使用方法名来调用。即`window.方法名();`和`方法名()`等效。
* 方法：
  1.  与**弹出框**有关的方法：
      1.  `alert();`:显示一段消息和一个确认按钮的警告框。
      2.  `confirm();`:显示带有一段消息以及确认按钮和取消按钮的对话框；
          1.  如果用户点击确认按钮，则方法返回true；
          2.  如果用户点击取消按钮，则方法返回false。
      3. `prompt();`:显示可提示用户输入的对话框
         1. 参数是提示信息
         2. 返回值是获取的用户输入的值。
  2. 与**打开关闭窗口**有关的方法：
     1. `open();`:打开一个新的浏览器窗口
        1. 参数是新窗口要加载页面的地址；
        2. 返回值是新的窗口的window对象；
     2. `close();`:关闭调用该方法的窗口对象的浏览器窗口
        1. 谁调用我，我关谁。
  3. 与**定时器**有关的方式
     1. `setTimeout();`：在指定的毫秒数后调用函数或计算表达式；
        1. 参数：
           1. **js代码**或者**方法对象**
           2. 毫秒值
        2. 返回值：唯一标识，用于作为取消定时器的参数
     2. `clearTimeout()`:取消由`setTimeout()`设置的定时器
        1. 参数：调用`setTimeout()`产生的返回值
     3. `setInterval()`:按照指定的**周期**(以毫秒记来调用函数或计算表达式；
         1. 参数：
              1. **js代码**或者**方法对象**
              2. 毫秒值
     4. `clearInertval()`:取消由`setInterval()`设置的定时器；
          1. 参数：调用`setInterval()`产生的返回值
```html
<script>
    var id = setInterval("fun()", 2000);
    clearInterval(id);
    var id2 = setInterval(fun, 2000);
    function fun(){
        alert("boom");
    }
</script>
```
* 属性：
  * 获取其它BOM对象
    * history;
    * location;
    * navigation;
    * screen;
    * 示例：
    * `var h1 = window.history;`与`var h2 = history;`等效。
  * 获取DOM对象
    * document等
    * 示例：`document.getElementById()`与`window.document.getElementById();`等效。

## Location对象

* 创建（获取）
  *  通过window对象的属性来获取。`var l1 = window.location;`与`var l2 = location;`等效。
* 方法：
  * `reload();`:重新加载当前文档
* 属性：
  * `herf`:设置或者返回完整的URL。
    * 获取：`var href = location.href;`
    * 设置：`location.herf = "http://baidu.com";`



# DOM

* 概念：Document Object Model 文档对象模型
* 功能：将标记语言文档的各个组成部分，封装为对象。可以使用这些对象，对**标记语言文档进行CRUD的动态操作**。
* DOM将HTMl表达为一个**树**型结构
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20201220211801.jpg)
* W3C DOM标准被分为3个不同的部分：
  * 核心DOM：针对**任何结构化文档**的标准模型。
    * Document:文档对象
    * Element:元素对象
    * Attribute:属性对象
    * Text：文本对象
    * Comment：注释对象
    * Node：节点对象，其余5个对象的父对象。
  * XML DOM：针对**XML文档**的标准模型；
  * HTML DOM：针对**HTML文档**的标准模型。

## 核心DOM

### Document对象

* 创建（获取）：在**HTML DOM模型**中可以使用**window对象**来获取
  * `window.document;`
  * `document`;
* 获取页面的**元素（标签）**对象
  * `getElementByID("id值");`:通过元素的ID获取元素对象，返回**一个**Element对象。因为id值一般是唯一的。
  * `getElementsByTagName("标签名");`:根据元素名称（即html标签名）获取元素对象们。返回值是一个**数组**。
  * `getElementsByClassName("class属性值);`:根据class属性值来获取元素对象们。返回值是一个数组。
  * `getElmentsByName("name属性值");`:根据name属性值来获取元素对象们。返回值是一个数组。
  * 示例：
```html
<div>div</div>
<script>
var div = document.getElementsByTagName("div");
alert(div.length);
</script>
```
* **创建**其它**DOM对象**
  * `createAttribute(name);`：创建具有指定名称的属性节点，并返回新的Attr对象。
  * `createComment();`：创建注释节点。
  * `creatElement();`：创建**元素节点**
  * `createTextNode();`:创建文本节点
  * 示例：`var table = document.createElement("table");`
* 操作Element对象：
  1. 修改属性值：
    * 明确获取的对象是什么元素类型；
    * 通过API查看对象里有哪些属性；
    * 通过`element.属性 = ...`的方式修改属性值。
  2. 修改标签内容：
    1.获取元素对象
    2.使用innerHTML属性修改标签体内容

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

</head>
<body>

<h1 id="title">悔创阿里杰克马</h1>
<img id="light" src="img/off.jpg">
<script>
    var light = document.getElementById("light");
    alert("我要换图片")；
    light.src="img/on.jpg";
    var title = document.getElementById("title");
    alert("我要换标题");
    title.innerHTML="不识妻美刘强东";
</script>
</body>
</html>
```   

### Elment对象

* 获取（创建）：通过**doucument**来获取和创建。
* 方法：
  * `removeAttribute();`:删除属性
  * `setAttribute();`:设置属性
  * 示例：
```html
<a>试一试</a>

<script>
var element_a = document.getElmentsByTagName("a")[0];
element_a.setAttribute("href", "https://www.baidu.com");
element_a.removeAttribute("href");
</script>
```

## 事件

* 功能：某些组件被执行了某些操作后，触发某些代码的执行。
* 绑定事件：
  1. 直接在html标签上，指定事件的属性（操作），属性值就是**js代码**。
     1.  事件：`onclicks`-- 单击事件
     2.  示例：`<img src="img/on.gif" onclicks="alert("我被点了");">`
  2. 通过js获取元素对象，指定事件属性，设置一个**函数**。
     1. 示例：
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

</head>
<body>

<img id="light" src="img/off.jpg" >
<script>
    function fun() {
      alert("我被点了");
    }

    var light = document.getElementById("light");
    light.onclicks=fun;
</script>
</body>
</html>
```