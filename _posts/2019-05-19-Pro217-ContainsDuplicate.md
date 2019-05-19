---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem217 Contains Duplicate 		# 标题 
subtitle:    #副标题
date:       2019-05-19				# 时间
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
Given an array of integers, find if the array contains any duplicates.  

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.  

Example 1:    

Input: [1,2,3,1]    
Output: true   

# 解题思路
就是最简单的两层for循环，这个没什么可说的。  

## 代码一
```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        for (int i = 0; i < nums.length; i++) {
            for (int index = i + 1; index < nums.length; index++) {
                if (nums[i] == nums[index]){
                    return true;
                }
            }
        }
        return false;
    }
}
```
## 效率探究
Runtime: 331 ms, faster than 6.85% of Java online submissions for Contains Duplicate.  
Memory Usage: 41.2 MB, less than 74.78% of Java online submissions for Contains Duplicate.  

# 解题思路
因为HashSet,不能存放重复的值，所以一旦有重复的值，就```return true```就可以了  

##代码二
```
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> a = new HashSet<>(2 * nums.length);
        for (int i: nums){
            if (!a.add(i)) return true;
        }
        return false;
    }
}
```
## 效率探究
Runtime: 4 ms, faster than 96.59% of Java online submissions for Contains Duplicate.  
Memory Usage: 41.3 MB, less than 71.70% of Java online submissions for Contains Duplicate.
## 小感想
**注意：感觉最近经常看到HashSet,HashMap,List之类的使用，这几天有空补一补这方面的知识。**