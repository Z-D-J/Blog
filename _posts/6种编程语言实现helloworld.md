---
title: 6种编程语言实现helloworld
date: 2020-09-19 10:21:20
tags:
---

# c语言

* 环境：在linux上安装gcc工具。(具体见博客[Gcc基础](https://z-d-j.github.io/2020/07/28/GCC%E5%9F%BA%E7%A1%80/))
* 程序源代码：
```c
#include <stdio.h>

int main() {

    printf("Hello World! I'm 20191091615004 张杰\n");

    return 0;
}
```
* 实现截图：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20200919104340.jpg)

# Python

## 环境：
* 在linux上编译安装Python3。（半年前装的，不好搞截图了。。。）
* 从官网下载Python3的压缩包。
* 解压缩到指定目录；
* 进入到该目录下，使用命令` ./configure --prefix=/usr/local/python3`;
* 之后`make`一下（make是运行Python3的包里的Makefile文件，自动进行编译安装）,记忆中这个过程耗时有一丢丢的长。
* 最后`make install`，完成安装。
* 在命令行输入`python3 --version`来查看安装的版本。
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20200919105429.jpg)

## helloworld实现

* 源代码（Python就一句。。。）
```python
print("hello world! I'm 2019091615004 张杰")
```
* 实现截图：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20200919110141.jpg)

# Java

## 环境

* Java的环境在Windows上需要去官网下载jdk并安装，然后修改环境变量。当然还可以直接下载安装idea这种IDE，什么都不用做了，直接编程就完事儿。在linux上就更简单啦，直接一波`sudo apt-get install openjdk-14-jdk`就搞定（openjdk对于我这种菜鸡来说应该完全够了/哈哈），然后使用`java --version`查看安装的版本以及是否安装成功。
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20200919110845.jpg)

## helloworld实现

* 程序源代码
```java

public class Hello {

    public static void main(String[] args) {
        System.out.println("hello world! I'm 2019091615004 张杰");
    }
}
```

* 实现截图：
![](https://gitee.com/zhangjie0524/picgo/raw/master/img/20200919112209.jpg)
（不过y1s1,除了打helloworld，其它程序还是用idea香，Java补全不行是真的难受）

