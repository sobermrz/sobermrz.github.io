---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem121 Best Time to Sell Stock	# 标题 
subtitle:    #副标题
date:       2019-05-20				# 时间
author:     Ruizhi Ma 						# 作者
header-img:              	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Leetcode刷题
    - Array
    - 难度：易
---

# 题号：
## 问题描述
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

Example 1:

Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.
Example 2:

Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.

# 解决思路一
思路很简单，分两步
1. 第一次for循环遍历数组
2. 内for循环，当前值以后的所有值
3. 在保证第二次遍历的值大于第一次遍历的值的前提下，计算出最大利润

## 问题解惑
我一开始把定义max是定义成```int max = Integer.MIN_VALUE```，后来想了想，应该直接定义成0，因为如果出现后面的全都小于前面的值，return的时候答案应该是0，所以直接max初始等于0，就可以返回回去当output了。

## 代码
```java
class Solution {
    public int maxProfit(int[] prices) {
       if (prices == null || prices.length < 1){
            return 0;
        }
        int max = 0;

        //traversing the array to get the buy price
        for (int i = 0; i < prices.length; i++) {
            int buy = prices[i];
            //traversing elements after the buy price
            for (int j = i; j < prices.length; j++) {
                int sell = prices[j];

                //count the max profit
                if (buy < sell){
                    int profit = sell - buy;
                    if (profit > max){
                        max = profit;
                    }
                }
            }
        }
        return max;
    }
}
```
## 效率探究
Runtime: 106 ms, faster than 10.51% of Java online submissions for Best Time to Buy and Sell Stock.

Memory Usage: 37.9 MB, less than 58.95% of Java online submissions for Best Time to Buy and Sell Stock.

# 解决思路二
一次循环，一边找最小值，一边同时算最大利润。

## 代码
```java
class Solution {
    public int maxProfit(int[] prices) {
       int maxPro = 0;
        int minPrice = Integer.MAX_VALUE;

        for (int price:
             prices) {
            minPrice = Math.min(minPrice, price);
            maxPro = Math.max(maxPro, price - minPrice);
        }

        return maxPro;
    }
}
```
## 效率探究
Runtime: 1 ms, faster than 79.80% of Java online submissions for Best Time to Buy and Sell Stock.

Memory Usage: 35.8 MB, less than 76.52% of Java online submissions for Best Time to Buy and Sell Stock.

## 小感想
**注意：现在还是见得题太少，做的题太少，遇到很多问题都第一时间用解法一的思路暴力求解，暂时还做不到有更优化的方法。不过不着急，边做边学吧，做一题，懂一题，一步步来。**