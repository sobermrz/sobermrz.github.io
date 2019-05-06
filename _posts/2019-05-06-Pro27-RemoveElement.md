---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem27 RemoveElement				# 标题 
subtitle:    #副标题
date:       2019-05-06 				# 时间
author:     Ruizhi Ma 						# 作者
header-img:              	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Leetcode刷题
---

# 题目类型：Array 难度：易 题号：27

## 问题描述
Given an array nums and a value val, remove all instances of that value in-place and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

Example 1:

Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.

It doesn't matter what you leave beyond the returned length.

## 解决思路
思路没什么可说的，但要注意 nums[res++] = nums[i] 这个，应该先执行数组赋值，再执行res++操作。

### 代码
package leetcode;

public class RemoveElement {
    public static int removeElement(int[] nums, int val){
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int res = 0;
        int[] save;
        for (int i = 0; i < nums.length; i++){
            if (nums[i] != val){
                nums[res++] = nums[i];
            }
        }
        return res;
    }
}
