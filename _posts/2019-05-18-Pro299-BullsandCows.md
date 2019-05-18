---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem299 BullsandCows				# 标题 
subtitle:    #副标题
date:       2019-05-18				# 时间
author:     Ruizhi Ma 						# 作者
header-img:              	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Leetcode刷题
    - Array
    - 难度：中
---

# 题号：
## 问题描述
You are playing the following Bulls and Cows game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.

Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows. 

Please note that both secret number and friend's guess may contain duplicate digits.

Example 1:

Input: secret = "1807", guess = "7810"

Output: "1A3B"

Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.
Example 2:

Input: secret = "1123", guess = "0111"

Output: "1A1B"

Explanation: The 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow.

## 解决思路
1. 遍历数组，记录unbulls的个数(最后用原数组长度减去unbulls就得到bulls的值)  
2. 创建两个新的数组用于保存两个旧的数组unbulls的数值  
3. 两层for循环分别比较两个新数组，一旦有相等的，cows加1  
4. return bulls和cows  

## 问题解惑
1. 我一开始理解错了题目，重复的是不计算的cows，比如‘10132’和‘13111’，这个里面除了第一位的1记为了cows,剩下的1只计算一次。这就是为什么count cows注释下的if判断为真之后要立即跳出的原因，防止重复计数。同时已经记为cows的值，要设置为999，也是为了重复计数。  
2. count cows的两个for循环一定是```i < unbulls```和```j < unbulls```，因为新数组的有效长度并不是```.length```出来的，因为初始的时候是用原数组的长度给他设置的数组长度，但实际上并没有存满，而bulls真实的记录了长度   

## 代码
```java
class Solution {
    public String getHint(String secret, String guess) {
        //define new arrays in order to record unbulls numbers
        int[] secretInt = new int[secret.length()];
        int[] guessInt = new int[secret.length()];
        int unbulls = 0;

        //converse unbulls char into Int and record unbulls char into new arrays.
        for (int i = 0; i < secret.length(); i++) {
            if(secret.charAt(i) != guess.charAt(i)){
                secretInt[unbulls] = Integer.parseInt(secret.substring(i, i+1));
                guessInt[unbulls] = Integer.parseInt(guess.substring(i, i+1));
                unbulls++;
            }
        }

        //count cows
        int cows = 0;
        for (int i = 0; i < unbulls ; i++) {
            for (int j = 0; j < unbulls; j++) {
                if (secretInt[i] == guessInt[j]){
                    cows++;
                    guessInt[j] = 999;//prevent compared number from comparing again
                    break;
                }
            }
        }

        return secret.length() - unbulls + "A" + cows + "B";
    }
}
```

## 小感想
**注意：**