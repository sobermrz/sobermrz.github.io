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

## 问题解惑
我一开始很疑惑，为什么需要我返回的明明是res，但Leetcode给我的output却包含了remove之后的数组呢？并且，我尝试了一下，将 nums[res++] = nums[i]改成res++，看能不能通过测试，结果是不可以！！！当然，“不可以”我是理解的，因为题目说了length = 2, with the first巴拉巴拉。可为什么我明明只返回了res，但系统却能读取到我remove之后的数组呢（output给出的是我remove之后的数组）？  
原来玄机如下，题目也给出了说明：  
*Confused why the returned value is an integer but your answer is an array?*
*Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.*

### 代码
```java
package leetcode;

public class RemoveElement {
    public static int removeElement(int[] nums, int val){
        if (nums == null || nums.length == 0) {
            return 0;
        }

        int res = 0;
        for (int i = 0; i < nums.length; i++){
            if (nums[i] != val){
                nums[res++] = nums[i];
            }
        }
        return res;
    }
}
```
