---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem	283 MoveZores	# 标题 
subtitle:    #副标题
date:       2019-06-14				# 时间
author:     Ruizhi Ma 						# 作者
header-img:              	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Leetcode刷题
    - Sort
    - 难度：易
---

# 题号：
## 问题描述
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example:

Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
Note:

You must do this in-place without making a copy of the array.
Minimize the total number of operations.

## 解决思路
先遍历数组，用```count```对所有非0元素进行计数，并且将非0元素保存在```nums[count]```的位置，并且count+1。最后将数组剩余长度位置全部置0.

## 问题解惑
为什么可以将非0元素覆盖在```nums[count]```的位置？   
因为数组中夹杂着0，所以遇到非0元素，则最多覆盖元素本身；若遇到0，刚好覆盖掉0。

## 代码
```java
package leetcode;

public class MoveZores {
    public void moveZeroes(int[] nums) {
        int count = 0;
        for (int i:nums){
            if (i != 0) {
                nums[count] = i;
                count++;
            }
        }

        for (int i = nums.length - 1; i >= count ; i--) {
            nums[i] = 0;
        }
    }
}

```