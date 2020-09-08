---
title: Make a complier
date: 2020-09-04 11:03:55
tags:
---

# 第一步：制作一个计算器

* 第一步只需要制作出一个能够读入诸如"2+3"这样的字符串，并输出计算的结果即可。
* 思路：
  1. 接收键盘的输入；
  2. 接收的过程中，将识别字符是数字还是运算符。如果是数字就还要确定它的数据类型，例如整型或者其它。
  3. 将接收到的数字和运算符转化为程序内部的运算，得出运算结果。
  4. 输出运算结果。
```c
# include <stdio.h>
# include <stdlib.h>

int main()
{
  char *str, op;
  int i, j, *ch, *temp, e, n, l, k;

  str = malloc(sizeof(char) * 10);
  ch = malloc(sizeof(int) * 10);
  temp = malloc(sizeof(int) * 10);

  scanf("%s", str); //读入字符串

//分词存储
  for(i = 0, j = 0; str[i] != '\n'; i++){
  //是数字：
    if(str[i] <= '9' && str[i] >= '0'){
      temp[j] = str[i];
      j++;
    }
  //不是数字：
    else{
      op = str[i];
  //将temp中存储的数字转化一个数
      l = --j; //记录temp中存储有多少位数；
      for(k = 0; k <= l; k++){
        for(e = 1, n = j - k; n >= 0; n--)
          e *= 10;
        ch[0] += str[k] * e;
      }
      break;
    }
  }
  //将读入的第二个数存储起来
  for(i++, j = 0; str[i] != '\n'; i++){
    temp[j] = str[i];
    j++;
  }
  l = --j;
  for(k = 0; k <= l; k++) {
    for(e = 1, n = j - k; n >= 0; n--)
      e *= 10;
    ch[2] += str[k] * e;
  }

//计算结果并输出
if(op == '+')
  printf("%d", ch[0] + ch[2]);
else if(op == '-')
  printf("%d", ch[0] - ch[2]);
else if(op == '*')
  printf("%d", ch[0] * ch[2]);
else 
  printf("%f", (float)(ch[0] / ch[2]));

return 0;
}
```