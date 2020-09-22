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
# 拥有糖果最多的孩子 1431

* 题目：
---
给你一个数组 candies 和一个整数 extraCandies ，其中 candies[i] 代表第 i 个孩子拥有的糖果数目。

对每一个孩子，检查是否存在一种方案，将额外的 extraCandies 个糖果分配给孩子们之后，此孩子有 最多 的糖果。注意，允许有多个孩子同时拥有 最多 的糖果数目。

 

示例 1：

输入：candies = [2,3,5,1,3], extraCandies = 3
输出：[true,true,true,false,true] 
解释：
孩子 1 有 2 个糖果，如果他得到所有额外的糖果（3个），那么他总共有 5 个糖果，他将成为拥有最多糖果的孩子。
孩子 2 有 3 个糖果，如果他得到至少 2 个额外糖果，那么他将成为拥有最多糖果的孩子。
孩子 3 有 5 个糖果，他已经是拥有最多糖果的孩子。
孩子 4 有 1 个糖果，即使他得到所有额外的糖果，他也只有 4 个糖果，无法成为拥有糖果最多的孩子。
孩子 5 有 3 个糖果，如果他得到至少 2 个额外糖果，那么他将成为拥有最多糖果的孩子。

* java解法
---
* 先找到拥有糖果数量最多的孩子，将加上补充的糖果数后的与这个最大比较
```java
public class Candy {

    public List<Boolean> kidsWithCandies(int[] candies, int extraCandies) { //List<Boolean>是来自List接口的
        int max = candies[0];
        List<Boolean> most = new ArrayList<>();

        for (int i = 1; i < candies.length; i++) {
           // max = Math.max(candies[i-1]，candies[i]); 这种方法实际上每次只比较了两个数的大小，而不是整个数组的大小
            max = Math.max(candies[i], max); //每次和已知的最大值比较，可以避免计数变量的计算
        }


//     for(int i = 0; i < candies.length; i++) {
//       if(candies[i] + extraCandies >= max) {
//         most.add(true);
//        }
//            else {
//              most.add(false);
//            }
//        }
        //用foreach循环代替上面的普通for循环，因为计数变量i除了除了用来指示当前数组变量，没有任何作用。
        for (int candy : candies) {
                    if (candy + extraCandies >= max) {
                        most.add(true);
                    } else {
                        most.add(false);
                    }
                }

        return most;
    }
    //测试
      public static  void main(String[] args) {
        Scanner in = new Scanner(System.in);
        int Maxsize;
        System.out.println("输入孩子个数：");
        Maxsize = in.nextInt();
        int[] candies = new int[Maxsize];

        System.out.println("请输入每个孩子的糖果数量：");
        for (int i = 0; i < candies.length; i++) {
            candies[i] = in.nextInt();
        }

        System.out.println("输入增加的糖果：");
        int extraCandies = in.nextInt();

        Candy candy = new Candy();

        List<Boolean> most2 = candy.kidsWithCandies(candies, extraCandies);

        for(int i = 0; i < candies.length; i++) {
            System.out.print(most2.get(i) + " ");
        }

    }
```