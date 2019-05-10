---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem189 Rotate Array 				# 标题 
subtitle:    #副标题
date:       2019-05-10				# 时间
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
Given an array, rotate the array to the right by k steps, where k is non-negative.  

Example 1:  

Input: [1,2,3,4,5,6,7] and k = 3  
Output: [5,6,7,1,2,3,4]  
Explanation:  
rotate 1 steps to the right: [7,1,2,3,4,5,6]  
rotate 2 steps to the right: [6,7,1,2,3,4,5]  
rotate 3 steps to the right: [5,6,7,1,2,3,4]  
Example 2:  

Input: [-1,-100,3,99] and k = 2  
Output: [3,99,-1,-100]  
Explanation:   
rotate 1 steps to the right: [99,-1,-100,3]  
rotate 2 steps to the right: [3,99,-1,-100]  
Note:  

Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.  
Could you do it in-place with O(1) extra space?  

## 解决思路一
这是比较直接的做法，当然，代价就是需要重新开辟一个数组，内存效率比较低。开辟一个和原数组一摸一样的数组,然后将新开辟的数组每一个元素，放到旧数组对应下标加k的位置上去（注意需要取余运算一下，防止k大于nums.length）,然后原数组就是rotate之后的数组了。

## 问题解惑
一开始我把Leetcode自己给我的类方法```public void rotate(int[] nums, int k)```改成了```public void rotateArray```，结果Leetcode死活通不过，并且在for循环的那个地方报错：*cannot find symbol [in __Driver__.java] new Solution.rotate(param_1,param_2);*,我个人认为应该是Leetcode已经规定好的方法名和类名最好是不能动的，如果改变，则在遇到循环等需要用方法调用Java内置类库的时候，会因为找不到规定好的方法而无法调用。以后博客里面方法名我会谨遵Leetcode给定的，但是类名因为都是在IDEA里面写完粘过来的，所以类名我就不写成Public class Solution了。

## 代码

### 解法一
```java
package leetcode;

public class RotateArray {
    public void rotate(int[] nums, int k){
        //Judge the boundary condition
        if(nums.length == 0 || nums.length == 1){
            return;
        }

        //Create a new array which is the same as the original array to store rotated elements
        int[] newNums = new int[nums.length];
        for(int i = 0; i < nums.length; i++){
            newNums[i] = nums[i];
        }

        /*Every elements in the new array will be put into the original array.The putting method  
        is each element in the new array should be put into an new index, which equals to their index plus k mode  
        the length of nums, in the original array*/  
        int index = 0;
        for (int i = 0; i < nums.length; i++){
            index = (i + k) % nums.length;
            nums[index] = newNums[index];
        }
    }
}

```
## 效率探究
Leetcode给出的运行效率：  
Runtime: 1 ms, faster than 39.86% of Java online submissions for Rotate Array.  
Memory Usage: 36.2 MB, less than 67.61% of Java online submissions for Rotate Array.  


## 解决思路二


## 问题解惑


## 代码

### 解法二
```java

```


## 解决思路三


## 问题解惑


## 代码
### 解法三
```java

```

## 小感想
**注意：  **