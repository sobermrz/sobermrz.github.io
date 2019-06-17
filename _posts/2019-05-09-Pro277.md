---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem277 Find the Celebrity # 标题 
subtitle:    #副标题
date:       2019-05-09				# 时间
author:     Ruizhi Ma 						# 作者
header-img:              	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - Leetcode刷题
    - Array
    - 难度：中
---

# 题号：
## 问题描述
Suppose you are at a party with n people (labeled from 0 to n - 1) and among them, there may exist one celebrity. The definition of a celebrity is that all the other n - 1 people know him/her but he/she does not know any of them.

Now you want to find out who the celebrity is or verify that there is not one. The only thing you are allowed to do is to ask questions like: "Hi, A. Do you know B?" to get information of whether A knows B. You need to find out the celebrity (or verify there is not one) by asking as few questions as possible (in the asymptotic sense).

You are given a helper function bool knows(a, b) which tells you whether A knows B. Implement a function int findCelebrity(n), your function should minimize the number of calls to knows.

Note: There will be exactly one celebrity if he/she is in the party. Return the celebrity's label if there is a celebrity in the party. If there is no celebrity, return -1.

## 解决思路
题目给了一个knows API（我自己随便写了knows函数以便调用），由其作用可知knows（A,B）为真，A认识B；否则A不认识B。题目中说其他人都认识celebrity，而celebrity不认识其他人。由此可以推导出解决方案：  
1. 第一次遍历数组的时候knows(candidate, i)为真，说明candidate认识i，则candidate必定不是celebrity,而i未知，用来取代成为新的candidate；反之，candidate是否为celebrity不确定。第一遍遍历结束，我们来看一下结果：  
0 1 2 3 4 5 6 7 ... n-1  
假设遍历结束，留下4是candidate，可以确保4之前的所有人认识candidate；4之后的所有人，candidate并不认识他们。但是很明显，条件还不充分。
2. 第二步遍历的目的，则是确认candidate不认识4之前的所有人；4之后的所有人都认识candidate。

## 问题解惑
这是一道挺有趣的题目，想了一会的地方就是第一遍遍历结束之后，能确保的是什么，不能确保的是什么。这个地方想通了，这道题就挺好理解的了。对了，这个题，没有必要再创建一个数组了，直接用下标就可以代替了，所以上面说的遍历数组都是不严谨的说法，你们能理解就好啦~  
好像还是有童鞋纠结这个knows函数，还告诉我“celebrity和谁比都是true啊，这不对啊？？？”，拜托，knows函数是系统提供的API，至于它内部是怎么实现的，我们不用关心，我这里写```return true ```只是用来简化一下表示一下，所以不要纠结，重点把握好~

## 代码
```java
public class FindtheCelebrity {
    //Assumption: 1. if no celebrity exists, the result returns to -1
    //            2. if boundary conditions are not met, the result returns to -1
    public int findCelebrity(int n){
        //Boundary Jundgement
        if (n < 2) return -1;

        int candidate = 0;
        //After traversing the whole array, there should be only one person who may or may not be the celebrity left.
        for(int i = 1;i < n;i++){
            //If candidate knows i, then candidate cannot be the celebrity. So, i replace the initial candidate to be the new candidate.
            if(knows(candidate, i)) {
                candidate = i;
            }
        }

        //Traversing the array again to confirm whether the candidate is the celebrity or not.
        for (int i = 0; i < n; i++) {
            if (candidate == i){
                continue;
            }

            if (!knows(i, candidate) || knows(candidate, i)){
                return -1;
            }
        }

        return candidate;
    }

    //Simplify the knows API in order to be called
    public boolean knows(int a, int b){
        return true;
    }
}
```

## 小感想
**注意：看了一点别人写的东西，我觉得很重要的有两个地方。第一，自己有时候要对题目给定一些assuption，因为题目没有说明边界条件不满足的时候怎么处理；第二，我们以后做开发，不可能从无到有，很多时候都是拿到一些现有的接口进行develop，就像这个里面，题目给了一个knows的API，这也给我一个提醒，以后面试的时候，遇到问题，可以拆分，比如这个部分我可以先不考虑，而是假设我已经写完了这个部分，我封装好了，先拿来调用，接着写后面的东西。等后面的解决了，再回头来补充完成我假定的内容。最后，以后争取所有代码内的注释都用英文写，加油吧！**