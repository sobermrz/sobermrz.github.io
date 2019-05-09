---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem26 RemoveDuplicatesfromSortedArray				# 标题 
subtitle:    #副标题
date:       2019-05-07 				# 时间
author:     Ruizhi Ma 						# 作者
header-img:              	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Leetcode刷题
    - Array
    - 难度：易
---

# 题号：26
## 问题描述
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.

It doesn't matter what you leave beyond the returned length.
Example 2:

Given nums = [0,0,1,1,1,2,2,3,3,4],

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.

It doesn't matter what values are set beyond the returned length.

## 解决思路
因为是有序的，其实只要比较前后两个数是不是一样就好啦，一开始还很笨的在想要不要遍历整个数组，真是too young too simple.

## 问题解惑
其实一开始担心的是```java nums[res++] = nums[i]``` 这个写法，如果重新开辟一个数组写成```java arr[res++] = nums[i]```我是完全理解，没有问题的。主要一开始担心的就是（其实我也不知道要怎么准确描述我的担心，我尽力描述一下），因为要对原数组进行覆盖，而且是向前覆盖，那会不会影响判断当前数与之前数是否一致？即前一个数会不会被其他数覆盖，导致当前数判断失效？其实不必担心，我自己草稿纸画了一下，的确没有问题。但从理论角度想了一下，因为本身是有序的，所以不会把后面的数提前拿到前面覆盖，要拿也只可能拿当前数，不会有比它大的，比它小的呢？早就放到更前面去啦！

## 代码
```java
package leetcode;

public class RemoveDuplicatesfromSortedArray {
    public int removeDuplicates(int[] nums) {

        if(nums == null || nums.length == 0) return 0;

        int res = 1;
        for(int i = 1; i < nums.length; i++){
            if(nums[i] != nums[res - 1]){
                nums[res++] = nums[i];
            }
        }
        return res;
    }
}
```
**注意：强烈建议这题和Pro.80对比看一下，理解会加深很多！！！**