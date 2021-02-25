---
layout: w
title: C语言-字符串数组
date: 2021-02-25 17:05:47
tags:
---

# 二维数组实现字符串数组

* 创建一个二维数组，按照每行一个字符串(一维字符数组)的方式，将一系列字符串存入一个数组中。
* 示例：
```c
char planets[][8] = { "Mercury", "Venus", "Earth",
					  "Mars", "Jupiter", "Saturn",
					  "Urans", "Neptune", "Pluto" };
```
* 因为每一行字符串的长度是省略的，所以每一行的长度是系统自动确定的。在二维数组中，每一行的数组的长度是根据最长的数组的长度来确定的。如果有一些行的数据不够填满整行，那么C语言**会用空字符`\0`来填补，造成了空间浪费**。
* 可以理解为用这种方式创建的**二维数组都是矩形的**。

# 指针数组实现字符串数组

* 要想实现**参差不齐的二维数组**，需要使用**元素为指针的数组**。
* 建立一个**元素都是指向字符串的指针**的数组，来实现字符串数组。
* 示例：
```c
char *planets[] = { "Mercury", "Venus", "Earth",
					"Mars", "Jupiter", "Saturn",
					"Urans", "Neptune", "Pluto"};
```

# 字符串数组的应用：命令行参数

* 运行程序是需要提供一些信息，这些信息从命令行中提供，称为**命令行参数**（C语言中也叫程序参数）。
* 为了访问命令行参数必须将**main函数定义为含有两个特殊参数的的函数**：
  * `argc`参数：argc是参数计数的参数，为int型，用于记录**命令行参数的数量**。
  * `argv`参数：argv是**指向命令行参数的指针数组**，这些命令行参数以**字符串**的形式存储。
    * argv是`char *argv[]`型的，实质就是一个字符串数组。
    * `argv[0]`指向**程序名**；
    * `argv[1]`到`argv[argc - 1]`指向余下的命令行参数。
    * `argv[argc]`是一个附加元素，这个元素时钟是一个**空指针**。
* 示例：
```c
#include <stdio.h>
#include <string.h>

#define NUM_PLANETS 9

int main(int argc, char* argv[]) {
	char *planets[] = { "Mercury", "Venus", "Earth",
						"Mars", "Jupiter", "Saturn",
						"Urans", "Neptune", "Pluto" };
	int i, j;

	for (i = 1; i < argc; i++) {
		for (j = 0; j < NUM_PLANETS; j++) {
			if (strcmp(argv[i], planets[j]) == 0) {
				printf_s("%s is planet %d\n", argv[i], j + 1);
				break;
			}
				if (j == NUM_PLANETS) {
					printf_s("%s is not a planet\n", argv[i]);
				}
		}
	}
	return 0;
}
```

