---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem243 Shortest Word Distance		# 标题 
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
Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.  

For example,  
Assume that words = ["practice", "makes", "perfect", "coding", "makes"].  

Given word1 = "coding", word2 = "practice", return 3.  
Given word1 = "makes", word2 = "coding", return 1.  

Note:  
You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.  

## 解决思路
1. 循环查找比较的word1和word2，分别记录下index1和index2  
2. 比较index1和index2之差的绝对值，循环计算最小distance替换min  


## 代码
```java
package leetcode;

public class ShortestWordDistance {
        public int shortestDistance(String[] words, String word1, String word2) {
            int index1 = 0;
            int index2 = 0;
            int dis = 0;
            int min = Integer.MAX_VALUE;
            for (int i = 0; i < words.length; i++) {
                if (words[i].equals(word1)){
                    index1 = i;
                    for (int j = 0; j < words.length; j++) {
                        if (words[j].equals(word2)){
                            index2 = j;

                            //calculate the distance
                            dis = Math.abs(i-j);
                            
                            //find the min distance
                            if (dis < min){
                                min = dis;
                            }
                        }
                    }
                }
            }
            return min;
    }
}

```
## 代码改进
```java
package leetcode;

public class ShortestWordDistance {
        public int shortestDistance(String[] words, String word1, String word2) {

            int index1 = -1;
            int index2 = -1;
            int min = Integer.MAX_VALUE;

            for (int i = 0; i < words.length; i++) {
                if (words[i].equals(word1)) index1 = i;
                if (words[i].equals(word2)) index2 = i;
                if(index1 != -1 && index2 != -1){
                    min = Math.min(min, Math.abs(index1 - index2));
                }
            }
            return min;
    }
}

```

## 小感想
**注意：比较两个非基本数据类型的值的时候，要用```equals```函数比较，不能用```==```，因为```==```比较的是内存地址，而```equals```才是比较的内容。在这里用```==```，虽然结果没错（因为在底层存储数组的时候，比如说words数组之前有一个"practic"，然后再次存入"practice",Java会从缓冲区查找是否有该值，有的话会将该地址直接赋给第二个"practice"，所以这样做，如果两个值一样，地址也是一样的），但是原理上来讲，String[]不是基本数据类型，这样是比较在地址值，是不对的！！！**