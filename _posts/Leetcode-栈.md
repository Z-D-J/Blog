---
title: Leetcode-栈栈
date: 2021-02-06 12:49:16
tags:
---

# 删除最外层的括号 1021

* 题目：
---
有效括号字符串为空 ("")、"(" + A + ")" 或 A + B，其中 A 和 B 都是有效的括号字符串，+ 代表字符串的连接。例如，""，"()"，"(())()" 和 "(()(()))" 都是有效的括号字符串。

如果有效字符串 S 非空，且不存在将其拆分为 S = A+B 的方法，我们称其为原语（primitive），其中 A 和 B 都是非空有效括号字符串。

给出一个非空有效字符串 S，考虑将其进行原语化分解，使得：S = P_1 + P_2 + ... + P_k，其中 P_i 是有效括号字符串原语。

对 S 进行原语化分解，删除分解中每个原语字符串的最外层括号，返回 S 。

 

示例 1：

输入："(()())(())"
输出："()()()"
解释：
输入字符串为 "(()())(())"，原语化分解得到 "(()())" + "(())"，
删除每个部分中的最外层括号后得到 "()()" + "()" = "()()()"。
示例 2：

输入："(()())(())(()(()))"
输出："()()()()(())"
解释：
输入字符串为 "(()())(())(()(()))"，原语化分解得到 "(()())" + "(())" + "(()(()))"，
删除每个部分中的最外层括号后得到 "()()" + "()" + "()(())" = "()()()()(())"。
示例 3：

输入："()()"
输出：""
解释：
输入字符串为 "()()"，原语化分解得到 "()" + "()"，
删除每个部分中的最外层括号后得到 "" + "" = ""。

## java解法

* 法一：
  * 使用一个栈来压入左括号，并将最外层括号设置为`*`来表示，再设置一个StringBuilder来录入除最外层括号的括号。
  * 每一次栈遇到右括号就弹出，以此来逐个匹配括号，从而判断谁为最外层的括号。
```java

import java.util.Stack;

public class Solution {
    public String removeOuterParentheses(String S) {
        Stack<Character> stack = new Stack<>();
        StringBuilder stringBuilder = new StringBuilder();

        //遍历字符串
        for(char i : S.toCharArray()) {
            //如果栈不为空，则证明不是最外层的左括号，存入stringBulider
            if(i == '(' && !stack.isEmpty()) {
                   stringBuilder.append(i);
                    stack.push(i);
            }else if(i == '(' && stack.isEmpty()) {
                stack.push('*');
            } else { //如果为右括号，则栈中内容弹出，并根据边界记号来判断是否到边界，如果不是，则将右括号也存入stringBuilder
                char temp1 = stack.pop();
                if(temp1 != '*') {
                    stringBuilder.append(i);
                }
            }
        }
        return String.valueOf(stringBuilder);
    }

    public static void main(String[] args) {
        String s = "(()())(()(()))";
        Solution solution = new Solution();
        System.out.println(solution.removeOuterParentheses(s));
    }
}
```