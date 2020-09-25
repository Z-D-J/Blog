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
