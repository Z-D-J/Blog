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

# 重新排列数组 1470

* 题目：
---
1470. 重新排列数组
给你一个数组 nums ，数组中有 2n 个元素，按 [x1,x2,...,xn,y1,y2,...,yn] 的格式排列。

请你将数组按 [x1,y1,x2,y2,...,xn,yn] 格式重新排列，返回重排后的数组。

 

示例 1：

输入：nums = [2,5,1,3,4,7], n = 3
输出：[2,3,5,4,1,7] 
解释：由于 x1=2, x2=5, x3=1, y1=3, y2=4, y3=7 ，所以答案为 [2,3,5,4,1,7]

* Java解法：
---
* 法一：设置一个额外的数组，用来将重排后的数据记录；
```java
import java.util.Scanner;

public class Resort1470 {

    public int[] reshuffle(int[] nums, int n) {
        int i;
        int j;
        int[] result = new int[2 * n];

        for(i = 0, j = 0; j < n; i++, j++) {
            result[i] = nums[j];
            result[++i] = nums[n + j];
        }
        return result;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);

        System.out.println("请输入数组的的长度：");
        int n = in.nextInt() / 2;
        System.out.println("请输入数字：");
        int[] nums = new int[2 * n];
        for(int i = 0 ; i < nums.length; i++) {
            nums[i] = in.nextInt();
        }

        Resort1470 resort = new Resort1470();
        nums = resort.reshuffle(nums, n);

        for(int i = 0; i < nums.length; i++) {
            System.out.print(nums[i] + " ");
        }
    }
}
```
* 法二：

#  左旋转字符串 剑指offer 58-II

* 题目：
---
字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

 

示例 1：

输入: s = "abcdefg", k = 2
输出: "cdefgab"

* Java解法：
---
* 将该字符串分为两个子串，然后再反向连接起来
```java
import java.util.Scanner;

public class ReverseLeftWords {

    public String reverseLeftWords(String s, int n) {
         String str1 = s.substring(0, n); //读入从0到n（但是不包括下标为n的）
         String str2 = s.substring(n); //从n开始到最后（包括下标为n的）
         String  s1 = str2 + str1;//反向连接，达到左旋转的效果

         return s1;
// return s.substring(n) + s.substring(o, n);

    }

    public static void main(String[] args) {
        String s = " ";
        int n;
        Scanner in = new Scanner(System.in);

        System.out.println("请输入字符：");
        s = in.nextLine();

        System.out.println("请输入从哪里开始转：");
        n = in.nextInt();

        var reverse = new ReverseLeftWords();
        s = reverse.reverseLeftWords(s, n);

        for(int i = 0; i < s.length(); i++) {
            System.out.print(s.charAt(i) + " ");
        }

    }
}
```

# 好数对的数目 1512

* 题目
---
给你一个整数数组 nums 。

如果一组数字 (i,j) 满足 nums[i] == nums[j] 且 i < j ，就可以认为这是一组 好数对 。

返回好数对的数目。

 

示例 1：

输入：nums = [1,2,3,1,1,3]
输出：4
解释：有 4 组好数对，分别是 (0,3), (0,4), (3,4), (2,5) ，下标从 0 开始.

* java解法
---
* 法一：双重循环遍历数组，外层为数组这个计数循环，内层取寻找与当前元素相同的元素（但是只找当前位置之后的，避免重复计算）
```java
import java.util.Scanner;

public class NumPairs1512 {

    public int numIdenticalPairs(int[] nums) {
        int ans = 0;

        for(int i = 0; i < nums.length; i++) {
            for(int j = i + 1; j < nums.length; j++) { //每次统计相同的元素都是从当前位置向后遍历，这样就不会有重复的情况
                if(nums[i] == nums[j]) {
                    ans++;
                }
            }
        }
        return ans;
    }

    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        System.out.println("请输入数组长度：");
        int maxsize = in.nextInt();
        System.out.println("请输入数字：");
        int[] nums = new int[maxsize];

        for(int i = 0; i < nums.length; i++) {
            nums[i] = in.nextInt();
        }

        var pairs = new NumPairs1512();
        System.out.println("好数对有" + pairs.numIdenticalPairs(nums) + "对");
    }
}
```
* 法二：

