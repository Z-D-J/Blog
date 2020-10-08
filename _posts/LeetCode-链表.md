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


# 链表中倒数第k个结点 剑指offer22

* 题目：
---
输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。例如，一个链表有6个节点，从头节点开始，它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个节点是值为4的节点。

 

示例：

给定一个链表: 1->2->3->4->5, 和 k = 2.

返回链表 4->5.

* Java解法
---
* 数出链表的总结点个数，然后推出正序的排名。
```java
public static int kthtoLast(SinglyLinkedList head, int k) {
        int nums = 1;
        SinglyLinkedList node = head;
        
        //得出当前链表的总结点个数
        while (node.next != null) { 
            node = node.next;
            nums++;
        }

        int index = nums - k + 1; //根据逆序排名得出正序排名
        
        //找到要求的结点
        node = head;
        for (int i = 1; i < index; i++) {
            node = node.next;
        }

        return node.val;
    }
```

测试代码：
```java
public static void main(String[] args) {
        Scanner in = new Scanner(System.in);

        System.out.println("请输入一串数字，以-1结束：");
        SinglyLinkedList head = new SinglyLinkedList();
        KthtoLast.getIn(head);

        System.out.println("输入要返回倒数第几个数：");
        int k = in.nextInt();

        KthtoLast reverse = new KthtoLast();
        System.out.println("结果为: " + reverse.kthtoLast(head, k));


    }
}
```

# 从尾到头打印链表 剑指offer 06. 

* 题目：

---

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

 

**示例 1：**

```
输入：head = [1,3,2]
输出：[2,3,1]
```

* Java解法

  ---
  
* 法一：
	* 每次遍历到相对的最后一个结点，通过一个计数变量来判断是否到达了最后一个结点。	
  ```java
  public static int[] reversePrint(SinglyLinkedList head) {
          SinglyLinkedList node = new SinglyLinkedList();
          int nums = 1;
          int i = 0;
          node = head;
  
          //计算链表中有多少个元素
          //注意判断链表为空的情况
          if(node == null){
              nums = 0;
          }
          else {
              while (node.next != null) {
                  node = node.next;
                  nums++;
              }
          }
  
          int[] result = new int[nums];
  
          node = head;
  
          if(nums == 0) {
              return result;//当链表为空时直接返回一个空数组
          }
          else {
              do {
                  //每次从第一个结点开始遍历到最后一个结点，将最后一个结点的值存入数组中
                  //如果有三个数，只需循环两次便可达到最后一个结点
                  for(int j = 1; j < nums; j++) {
                      node = node.next;
                  }
                  result[i] = node.val;
                  node = head;
                  i++;
                  //将链表的长度减一，表示最后一个结点已经被输出了
                  nums--;
              } while(nums != 0);
  
              return result;
          }
  }
  //测试代码
  @Test
  public void testReversePrint() throws Exception {
      //设置测试链表为｛1， 3， 2｝
      SinglyLinkedList head = new  SinglyLinkedList();
      head.val = 1;
      SinglyLinkedList node1 = new SinglyLinkedList();
      head.next = node1;
      node1.val= 3;
      SinglyLinkedList node2 = new SinglyLinkedList();
    node2.val = 2;
	    node1.next = node2;
	
	    int[] result = new int[3];
	    result = SinglyLinkedList.reversePrint(head);
	    //预期结果为｛2，3，1｝
	    int[] exp = {2, 3, 1};
	    //断言判断结果是否为｛2， 3，1｝
	    Assert.assertArrayEquals(result, exp);
	} 
	```
	
* 法二：

  * 使用一个定长的数组，但是对数组的赋值是从逆向开始的。这样避免了对链表的逆转。

* 法三：‘’

  * 使用栈

# 移除重复结点 面试题02.01 

* 题目

  ---
  编写代码，移除未排序链表中的重复节点。保留最开始出现的节点。
  
  示例1:
  
   输入：[1, 2, 3, 3, 2, 1]
   输出：[1, 2, 3]
  
* Java解法

  ---
  * 法一：
  	* 将链表中的元素在逐个遍历时存入一个数组中，在遍历时进行比对，如果出现相同元素值，则跳过该元素

  ```java
  //删除链表中重复结点的方法
      public SinglyLinkedList removeDuplicateNodes(SinglyLinkedList head) {
  
          SinglyLinkedList node = head;
          int nums = 0;
  
          //计算链表中元素的个数
          while(node != null) {
              node = node.next;
              nums++;
          }
          //注意排除链表为一个空链表的情形（即head为一个null）
          if(nums == 0) {
              return head;
          }
  
          //用于储存已经读出的元素值的数组
          int[] temp = new int[nums];
          int i = 0;
          int j = 0;
  
          //遍历数组并跳过重复结点,将遍历的结果存入数组中
          node = head;
          while(node != null) {
              if(i == 0) {
                  temp[i] = node.val;
                  node = node.next;
                  i++;
              }
              else {
                  for( j = i - 1; j >= 0; j--) {
                      if(node.val == temp[j]) {
                          node = node.next;
                          nums--;
                          break;
                      }
                  }
                  if(j >= 0) {
                      continue;
                  }
                  else {
                      temp[i] = node.val;
                      node = node.next;
                      i++;
                  }
              }
          }
  
          //将数组中的结果重新存入链表中
          node = head;
          for(i = 0; i < nums - 1; i++) {
              node.val = temp[i];
              node = node.next;
          }
          //最后一个结点需要单独赋值，因为需要将它的next设为null
          node.val = temp[nums - 1];
          node.next = null;
  
          return head;
      }
  //测试用例
  /**
   *
   * Method:  removeDuplicateNodes(SinglyLinkedList head)
   *
   */
  @Test
  public void testRemoveDuplicateNodes() throws Exception {
      //创建测试链表为｛1，2，3， 3， 2，1｝
      SinglyLinkedList head = new  SinglyLinkedList();
      head.val = 1;
      SinglyLinkedList node1 = new SinglyLinkedList();
      head.next = node1;
      node1.val= 2;
      SinglyLinkedList node2 = new SinglyLinkedList();
      node2.val = 3;
      node1.next = node2;
      SinglyLinkedList node3 = new SinglyLinkedList();
      node3.val = 3;
      node2.next = node3;
      SinglyLinkedList node4 = new SinglyLinkedList();
      node4.val = 2;
      node3.next = node4;
      SinglyLinkedList node5 = new SinglyLinkedList();
      node5.val = 1;
      node4.next = node5;
  
      head = head.removeDuplicateNodes(head);
  
      SinglyLinkedList node = head;
      int nums = 0;
  
      //计算链表中元素的个数
      while(node != null) {
          node = node.next;
          nums++;
      }
  
      //用于储存读出的元素值的数组
      int[] temp = new int[nums];
      int i = 0;
      int j = 0;
  
      //遍历数组,将遍历的结果存入数组中
      node = head;
      while(node != null) {
          temp[i] = node.val;
          node = node.next;
          i++;
      }
  
      //预期结果
      int[] exp = {1, 2, 3};
  
      Assert.assertArrayEquals(temp, exp);
  
  }
  
  ```

  * 法二：
    * set集合去重
  * 法三：
    * 哈希表
  * 法四：
    * 位运算
  * 法五：
    * 双指针