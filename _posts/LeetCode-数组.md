---
title: LeetCode-数组
date: 2020-09-20 10:01:51
tags:
---

# 一维数组的动态和 1480

* 题目：
---
给你一个数组 nums 。数组「动态和」的计算公式为：runningSum[i] = sum(nums[0]…nums[i]) 。

请返回 nums 的动态和。

 

示例 1：

输入：nums = [1,2,3,4]
输出：[1,3,6,10]
解释：动态和计算过程为 [1, 1+2, 1+2+3, 1+2+3+4] 。

* Java解法
---

* 动态求和过程中，每一项都是前一项与自身之和。
* 第一个元素没有前一个元素，对它没有操作，所以直接从第二个元素开始遍历求和。
```java
import java.util.Scanner;

public class Sums {

    public int[] runningSums (int[] nums) {

        for(int i = 1; i < nums.length; i++) {
//            if(i == 0) {
//                continue;
//            }因为0是无需操作的，所以直接从1开始就好了
            nums[i] += nums[i-1] ;
        }
        return nums;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int Maxsize;
        System.out.println("输入数字个数：");
        Maxsize = in.nextInt();
        int[] nums = new int[Maxsize]; //Maxsize必须在在这里使用之前就初始化



        System.out.println("请输入数字：");
        for (int i = 0; i < nums.length; i++) {
            nums[i] = in.nextInt();
        }

        Sums run = new Sums();

        // nums = run.runningSums(nums);因为nums是引用（可以类似c语言的指针），所以nums传进函数的对象被修改了，但是nums依然指向那个对象，所以可以不用接收返回值
        run.runningSums(nums);

        for (int i : nums) { //此时的i不再是数组下标，在foreach循环中，是直接将数组元素的值赋给i
            System.out.print(i + " ");
        }
    }
}
```