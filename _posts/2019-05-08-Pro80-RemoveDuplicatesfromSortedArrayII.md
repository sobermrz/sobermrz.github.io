---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem80 RemoveDuplicatesfromSortedArrayII  # 标题 
subtitle:    #副标题
date:       2019-05-08 				# 时间
author:     Ruizhi Ma 						# 作者
header-img:              	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Leetcode刷题
    - Array
    - 难度：中
---

# 题目描述
Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

Given nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.

It doesn't matter what you leave beyond the returned length.
Example 2:

Given nums = [0,0,1,1,1,1,2,3,3],

Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively.

It doesn't matter what values are set beyond the returned length.

# 解题思路
这题和26题非常像，这一题也是更加加深了我对这个类型题目的理解。其实核心思想就是：用两个指针（姑且称之为指针吧），index用来定位，i用来遍历数组。判断的条件就是，如果遍历到的数（下标为i），和定位的数前一个(下标为 index-1)相等，并且定位数前一个(下标为 index-1)和定位数前前一个数（下标为 index-2）也相等，则说明有三个相等的数了，就跳过。此时index指向的下标还没有重新存入数，并且index是重新存入数的长度。

```java
package leetcode;

public class RemoveDuplicatesfromSortedArrayII {
    public int removeDuplicates(int[] nums) {
        if(nums.length <= 2){
            return nums.length;
        }

        int index = 2;
        for(int i = 2; i < nums.length; i++){
            if(!(nums[i] == nums[index - 1] && nums[index - 1] == nums[index - 2])){
                nums[index++] = nums[i];
            }
        }

        return index;
    }
}
```


