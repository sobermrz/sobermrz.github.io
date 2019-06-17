---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem 88 Merge Sorted Array 			# 标题 
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
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:

The number of elements initialized in nums1 and nums2 are m and n respectively.
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.
Example:

Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]

## 解决思路
首先，两个数组nums1和nums2是已经排序好的。所以思路就是从nums1和nums2末尾元素（nums1下标为m-1的是末尾元素）开始比较，较大者放入数组最后面，依次类推。当其中一个数组下标小于0时，则剩下数组的全部元素应该都是最小的，所以直接依次放入nums1最前面就完成了。

## 问题解惑
为什么最后注释掉一个while?  
因为没必要把i中最前面的元素再赋值给本身，多此一举啦！  

## 代码
```java
package leetcode;

public class MergeSortedArray {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int i = m - 1, j = n - 1, k = m + n - 1;

        while( i >= 0 && j >= 0){
            if (nums1[i] >= nums2[j]) {
                nums1[k] = nums1[i];
                i--;
                k--;
            }else{
                nums1[k] = nums2[j];
                j--;
                k--;
            }
        }

        //i < 0
        while (j >= 0){
            nums1[k] = nums2[j];
            j--;
            k--;
        }

        //j < 0
        /*while (i >= 0){
            nums1[k] = nums1[i];
            i--;
            k--;
        }*/
    }
}

```

## 注意
好像还有一个merge函数的做法，据说能加深对merge的了解，回头再来补充。  