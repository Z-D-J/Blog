---
title: Python
date: 2020-09-05 20:45:19
tags:
---
# python的特性

1. Python是一门解释性语言，无需编译和链接。
2. Python解释器是可以交互的，因此Python甚至可以用作桌面计算器。
3. Python是可扩展的，可以为Python的解释器添加内置函数和模块。

# python的注释

* Python中使用`#`做注释符，即使是在解释器的交互编程中也可以使用`#`注释符。

# 数据类型

## 数字

* 常用的数据类型有int、float，但是Python还有其它很多数据类型。例如复数类型（complex）,这种类型中使用j或者J代表复数部分，如`5+2j`.
* 基本运算
  * Python支持基本的`+`,`-`,`*`以及`/`，`%`的运算，但是和c语言不同的是，`/`默认的结果是浮点型。使用`//`可以做返回值为int型的除法运算（类似c语言的普通除法运算）.
  * Python还支持幂方运算`**`,`5**2`表示$5^2$；
  * python仍旧使用`=`为变量赋值，同c语言一样，Python中的变量在使用前必须先进行赋值。（但是在交互式编程中，Python内置了一个变量`_`,存储最近一个表达式的运算结果，这个变量无需赋值，便可直接使用，事实上，`_`是一个只读变量，对它赋值是没有意义的。）
  * python的赋值可以进行多重赋值，例如：`a, b = 0, 1`相当于`a = 0, b = 1`

## 字符串

* 字符串可以用单引号`''`或者双引号`""`表示;
* 引号可以用`\`来转义。
* 字符串可以用`+`连接，如`'zhang'+'jie'`合为`'zhangjie'`.
* 字符串可以用`*`重复输出。`'zj'*3`即为`'zjzjzj'`。
* 字符串可以被索引，进行类似c语言的取出字符串的中字母的操作。如：`word = 'python`, `word[0] == 'p'`;索引可以为负数，这会从右边开始索引。如：`word = 'python'`,`word[-1] = 'n'`(负索引是从-1开始，而不是0)。
* 字符串可以被切片。如`word = 'python'`,则`word[0:2] = 'py'`,包含起始的字符，不包含末尾的字符。切片可以省略，省略左边，默认为从0开始，省略右边，则默认到末尾。如`word[:3] = 'pyt'`,`word[1:] = 'ython'`。
* 字符串是不可变的，不可以被修改。如果需要修改，只能创建一个新的字符串，并在创建的过程中，将修改加进去。

## 列表

* 列表类似c语言的数组。但是列表中的元素不需要是同一类型。
* 列表的赋值：如`list1 = [1, 2, 3, 4, 5]`， `list2 = [1, 'a', 2, 'b', 3]`.
* 同字符串一样，列表也可以被切片和索引。
* 同字符串一样，列表也支持使用`+`进行连接,使用`*`进行重复。但是连接和重复的对象都必须是列表，返回的结果也是列表。
* 与字符串不同的是，列表中的元素是可以修改的。可以利用赋值操作对列表中某个元素进行修改。
* 可以使用append（）方法，在列表后面加元素。(括号中放需要加的元素。)
* 列表中可以嵌套列表。
* 使用函数len（），可以得到列表或者字符串的长度。如；`len(list1)`的结果为5.
  
# python的流程控制

## if语句

* 类似c语言中的if语句，但是python省去了条件外面的括号，而是用冒号`:`来表示（就像c语言不能忘记括号一样，python也不能忘记冒号），并将`else if`合成了一个`elif`关键字（但是还是有单独的`else`)。如：
```python
 x = (int)(input()) #input读取键盘的输入，但是默认读入的类型是字符串型，需要强制转换为数字整型
 
 if x < 0:
         x = 0
         print(x)
 elif x == 0:
         x = -1
         print(x)
 else:
         x = 1
        print(x)
```

* python条件语句内部的语句不是用花括号`{}`来括起来，而是直接用缩进来表示包含关系。所以这种带有控制语句的代码最好不直接在解释器中写。

## for语句

* 与c语言的for循环不同的是，python的for循环没有控制条件，它自动停止的。例如
```python 
words = ['zhang', 'jie']

for word in words:
  print(word)
```
* for循环常用来遍历列表或者字符串等序列，循环会在序列尾部自动结束。而在示例程序中的`word`变量是定义的列表序列中的单个元素。注意`for...in...`的格式。

## range()函数

* range()会生成一个指定长度的链表，例如：`range(10),会生成一个从0到9的序列，即参数10是指定生成的链表的长度，默认情况下，这个等差链表是从0开始的。
* 可以指定range生成的链表的起始和结束，例如：`range(5, 10)`会生成一个从5到9的链表。
* 可以指定链表的步长（即公差，可以为负数）。例如：`range(0, 10, 3)中的第一个参数是起始的数，结束的数为10（永远不会包含指定的结束数），3为步长`,结果为0， 3， 6， 9。可以把步长设置为负数，形成从大到小的链表。例如`range(-10, -100, -30)`,结果-10，-40，-70。

## break和continue语句，以及循环中的else子句

* 在for循环中，else放在break语句之后，在没有执行break时，执行else语句。break的作用仍然与c语言类似，用于跳出最近的for或while循环。示例：
```python
>>> for n in range(2, 10):
...     for x in range(2, n):#第一次循环，range（2,2)是没有值的,解释器不会输出任何内容
...         if n % x == 0:
...             print(n, 'equals', x, '*', n//x)
...             break
...     else:
...         # loop fell through without finding a factor
...         print(n, 'is a prime number')
...
2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3
```
*continue语句与c语言中基本一样，它表示跳过continue语句中后面所有的当前循环的语句（到循环尾），从而直接进入下一次迭代。示例：
```python
>>> for num in range(2, 10):
...     if num % 2 == 0:
...         print("Found an even number", num)
...         continue
...     print("Found a number", num)
Found an even number 2
Found a number 3
Found an even number 4
Found a number 5
Found an even number 6
Found a number 7
Found an even number 8
Found a number 9
```

## pass语句

* pass语句就像它的名字一样，读到它时，什么也不做，直接过去就行。

# 函数

## 函数定义

* 使用`def`定义函数，`def`后接函数的名字，以及她的形参列表，最后就像大多数功能语句一样，以`:`开启函数体。
* 函数体的书写必须必须全部相对定义缩进。示例：

```python
>>> def fib(n):    # write Fibonacci series up to n
...     """Print a Fibonacci series up to n."""
...     a, b = 0, 1
...     while a < n:
...         print(a, end=' ')
...         a, b = b, a+b
...     print()
...
>>> # Now call the function we just defined:
... fib(2000)
0 1 1 2 3 5 8 13 21 34 55 89 144 233 377 610 987 1597
```
* 函数体的第一行可以写字符串（用三个双引号包起来），来对该函数做说明，相当于另一种形式的注释。

## 函数调用

* 直接输入函数的名字并给他传递实参即可，例如`fib(10)`,即是对前文函数的调用。
* 函数名可以直接赋值给其它变量。如
```python 
f = fib

f(10)
```
与直接`fib(10)`效果一样。

# 列表的高级用法

## 列表

* `list.append（x）`在列表的后面加上一个元素x。
* `list.extend(L)`将一个给定列表（L）中的元素全部都加到另一个列表里（list）.
* `list.insert(i, x)`在列表的指定元素之前插入元素。其中第一个参数是指定列表中元素的索引，第二个参数是要插入的值。如，`list.insert(0, 5)`是在整个列表前插入一个5.
* `list.remove(x)`删除列表中值为x的第一个元素，如果没有这样的元素，则会返回错误。





