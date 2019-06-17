---
layout:     post   				    # 使用的布局（不需要改）
title:      Problem299 BullsandCows				# 标题 
subtitle:    #副标题
date:       2019-05-18				# 时间
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
You are playing the following Bulls and Cows game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position (called "bulls") and how many digits match the secret number but locate in the wrong position (called "cows"). Your friend will use successive guesses and hints to eventually derive the secret number.

Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows. 

Please note that both secret number and friend's guess may contain duplicate digits.

Example 1:

Input: secret = "1807", guess = "7810"

Output: "1A3B"

Explanation: 1 bull and 3 cows. The bull is 8, the cows are 0, 1 and 7.
Example 2:

Input: secret = "1123", guess = "0111"

Output: "1A1B"

Explanation: The 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow.

## 解法一
### 解决思路
1. 遍历数组，记录unbulls的个数(最后用原数组长度减去unbulls就得到bulls的值)  
2. 创建两个新的数组用于保存两个旧的数组unbulls的数值  
3. 两层for循环分别比较两个新数组，一旦有相等的，cows加1  
4. return bulls和cows  

### 问题解惑
1. 我一开始理解错了题目，重复的是不计算的cows，比如‘10132’和‘13111’，这个里面除了第一位的1记为了cows,剩下的1只计算一次。这就是为什么count cows注释下的if判断为真之后要立即跳出的原因，防止重复计数。同时已经记为cows的值，要设置为999，也是为了重复计数。  
2. count cows的两个for循环一定是```i < unbulls```和```j < unbulls```，因为新数组的有效长度并不是```.length```出来的，因为初始的时候是用原数组的长度给他设置的数组长度，但实际上并没有存满，而bulls真实的记录了长度   

### 代码
```java
class Solution {
    public String getHint(String secret, String guess) {
        //define new arrays in order to record unbulls numbers
        int[] secretInt = new int[secret.length()];
        int[] guessInt = new int[secret.length()];
        int unbulls = 0;

        //converse unbulls char into Int and record unbulls char into new arrays.
        for (int i = 0; i < secret.length(); i++) {
            if(secret.charAt(i) != guess.charAt(i)){
                secretInt[unbulls] = Integer.parseInt(secret.substring(i, i+1));
                guessInt[unbulls] = Integer.parseInt(guess.substring(i, i+1));
                unbulls++;
            }
        }

        //count cows
        int cows = 0;
        for (int i = 0; i < unbulls ; i++) {
            for (int j = 0; j < unbulls; j++) {
                if (secretInt[i] == guessInt[j]){
                    cows++;
                    guessInt[j] = 999;//prevent compared number from comparing again
                    break;
                }
            }
        }

        return secret.length() - unbulls + "A" + cows + "B";
    }
}
```
###效率探究
Runtime: 9 ms, faster than 12.10% of Java online submissions for Bulls and Cows.  
Memory Usage: 36.1 MB, less than 81.97% of Java online submissions for Bulls and Cows.  

## 解法二  
### 解决思路  
1. 创建一个bucket数组，目的是借用桶排序的思想（emmm...虽然暂时还没学桶排序），进行多存储。对于secret中出现的数（比如说3），在bucket数组中，将下标为3的元素自增一次。对于guess中出现的数（比如说5），在bucket数组中，将下标为5的元素自减一次。  
2. 在自增自减之前，还要对bucket中改下标的元素进行两次if检查。第一次if检查，如果bucket数组中```secret.charAt(i) - '0'```下标的元素小于0，则说明guess数组中出现过该元素（做了自减操作），则说明secret和guess两个数组有值相等，但位置不同的元素存在。所以此时cow++。对于另一个if检查，同理。

### 问题解惑
问：为什么bucket数组长度是10呢？  
答：因为secret和guess数组中的单个元素是0~9的，bucket的下标和前两个数组的元素值对应，所以长度为10刚好够用。   
问：这样的算法，为什么可以避免重复数的比较？    
答：我姑且称这种叫做“抵消算法”，同一个数，secret中有几次则自增几次，guess有几次则自减几次。会互相抵消，不会造成重复配对的情况。  

### 代码
```java
class Solution {
    public String getHint(String secret, String guess) {
        int unbulls = 0;
        int cows = 0;
        //create a bucket array in order to mark
        int[] bucket = new int[10];

        for (int i = 0; i < secret.length(); i++) {
            if(secret.charAt(i) != guess.charAt(i)){
                unbulls++;//record unbulls number

                //check whether current number has been occurred in the other array.
                //if it has been occurred before, cows++
                if (bucket[secret.charAt(i) - '0'] < 0) cows++;
                if (bucket[guess.charAt(i) - '0'] > 0) cows++;

                //using positive and negative numbers in bucket array to mark numbers occurred in the two arrays, respectively.
                bucket[secret.charAt(i) - '0']++;
                bucket[guess.charAt(i) - '0']--;
            }
        }

        int bulls = secret.length() - unbulls;

        return bulls + "A" + cows + "B";
    }
}
```
### 效率探究
Runtime: 2 ms, faster than 58.72% of Java online submissions for Bulls and Cows.  
Memory Usage: 35.4 MB, less than 87.55% of Java online submissions for Bulls and Cows.  
### 小感想
**注意：可能我太笨了，瞪着眼睛看了好几遍没看懂这种方法，然后用IDE调试，一步步跟着走，大概了解了流程，然后再草稿纸上举例再验算一遍，瞬间懂了，实在是叹服这种方法的巧妙！！！所以以后看不懂的代码，先用IDE调试，然后看参数的变化，说不定就很快能懂啦！建议先用IDE调试，跟着走一遍，再看看我写的解题思路和问题解惑，一定能有更深的体会！！！**