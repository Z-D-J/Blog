---
title: LeetCode-链表
date: 2020-09-25 11:20:59
tags:
---

# 删除中间结点 面试题02.03

* 题目：
---
实现一种算法，删除单向链表中间的某个节点（即不是第一个或最后一个节点），假定你只能访问该节点。

 
示例：

输入：单向链表a->b->c->d->e->f中的节点c
结果：不返回任何数据，但该链表变为a->b->d->e->f

* java解法
---
* 因为只知道当前结点以及这个结点之后的所有结点，所以无法直接删除当前结点。
* 可以将当前结点后的一个结点的值赋给当前结点，然后删除之后的结点，达到删除当前结点的等效效果。（我变成你，再杀了你，就相当于杀了我自己）。
```java
import java.util.Scanner;

public class SinglyLinkedList {
    //定义单链表结点
    int val = 0;
    SinglyLinkedList next = null; //储存下一个结点的引用

    SinglyLinkedList(int x) {
        this.val = x;
    }
    
    SinglyLinkedList() {}

    //定义删除某一结点的方法
    public void deleteNode(SinglyLinkedList node) {
        node.val = node.next.val;
        node.next = node.next.next;
    }

    //测试删除的方法
    public static  void main(String[] args) {
        Scanner in = new Scanner(System.in);
        
        //读取数字组，并存入链表中
        System.out.println("请输入一串数字，以-1结束：");
        int temp = in.nextInt(); 
        SinglyLinkedList fnode  = new SinglyLinkedList(temp);
        SinglyLinkedList list = new SinglyLinkedList();
        list.next = fnode; //创建一个头结点
        while (temp != -1) {
            temp = in.nextInt();
            SinglyLinkedList lnode = new SinglyLinkedList(temp);
            fnode.next = lnode;
            fnode = lnode; //使当前结点始终为链表末尾的结点
        }

        //找到要删除的结点
        System.out.println("输入要删除的数字：");
        SinglyLinkedList node = list.next;
        int delete = in.nextInt();
        while (node.val != delete) {
            node = node.next;
        }

        //删除结点并打印新链表的结果
        node.deleteNode(node);
        node = list.next;
        while(!(node.next == null)) {
            System.out.print(node.val + " ");
            node = node.next;
        }
    }
}
```

# 二进制链表转整数 1290

* 题目
---
给你一个单链表的引用结点 head。链表中每个结点的值不是 0 就是 1。已知此链表是一个整数数字的二进制表示形式。

请你返回该链表所表示数字的 十进制值 。

 

示例 1：



输入：head = [1,0,1]
输出：5
解释：二进制数 (101) 转化为十进制数 (5)

* java解法
---

* 法一：
```java
import java.util.Scanner;

public class BtoD  {
    public int binaryToDecimal(SinglyLinkedList head) {
        int nums = 0;
        int result = 0;
        int temp = 0;
        int index = 1;
        SinglyLinkedList node = head;
        for( nums = 0; node != null; node = node.next, nums++);

        node = head;
        for(; node != null; ) {
            temp = nums;
            for(index = 1; temp - 1 > 0; temp--) {
                index *= 2;
            }
            result += index * node.val;
            node = node.next;
            nums--;
        }

        return result;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);

        System.out.println("请输入一串二进制数字，以-1结束：");
        int temp = in.nextInt();
        SinglyLinkedList fnode  = new SinglyLinkedList(temp);
        SinglyLinkedList head = fnode; //保存头结点
        temp = in.nextInt();
        while (temp != -1) {
            SinglyLinkedList lnode = new SinglyLinkedList(temp);
            fnode.next = lnode;
            fnode = lnode; //使当前结点始终为链表末尾的结点
            temp = in.nextInt();
        }

        BtoD converse = new BtoD();
        System.out.println("十进制的结果为：" + converse.binaryToDecimal(head));
    }
}
```

* 法二：使用位运算