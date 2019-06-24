---
layout:     post   				    # ʹ�õĲ��֣�����Ҫ�ģ�
title:      CS61b Lecture 1			# ���� 
subtitle:   Java�����﷨�ع���ϰ       #������
date:       2019-6.23			# ʱ��
author:     Nuo Xu 						# ����
header-img:              	#��ƪ���±��ⱳ��ͼƬ
catalog: true 						# �Ƿ�鵵
tags:								#��ǩ
    - CS61b
    
---
# ѧϰ����
HW 0: A Java Crash Course

## ��ϰ1
1.��ӡָ��������������
2.�ҵ�һ�������е����ֵ

### ����
```java
public class learning {
    public static void main(String[] args) {
        drawTriangle(10);
        int[] numbers = new int[]{9, 2, 15, 2, 22, 10, 6};
        System.out.println(max(numbers));
    }
    /**��ӡָ��������������*/
    public static void drawTriangle(int N){
        for(int x = 1;x<N + 1;x++){
            for(int y = x;y>0;y--){
                System.out.print("*");
            }
            System.out.println();
        }
    }
    /** Returns the maximum value from m. */
    public static int max(int[] m) {
        int max = 0;
        int value = 0;
        if (m.length == 1){
            return m[0];
        }else{
            for(int i = 0;i<m.length-1;i++){
                int s = m[i] - m[i+1];
                if (s>0){
                    value = m[i];
                }else {
                    value = m[i+1];
                }
                int t = max - value;
                if (t>0){
                    max = max;
                }else {
                    max = value;
                }
            }
        }
        return max;
    }
}
```
## ��ϰ2
Write a function windowPosSum(int[] a, int n) that replaces each element a[i] with the sum of a[i] through a[i + n], but only if a[i] is positive valued. If there are not enough values because we reach the end of the array, we sum only as many values as we have.

For example, suppose we call windowPosSum with the array a = {1, 2, -3, 4, 5, 4}, and n = 3. In this case, we��d:

Replace a[0] with a[0] + a[1] + a[2] + a[3].
Replace a[1] with a[1] + a[2] + a[3] + a[4].
Not do anything to a[2] because it��s negative.
Replace a[3] with a[3] + a[4] + a[5].
Replace a[4] with a[4] + a[5].
Not do anything with a[5] because there are no values after a[5].
Thus, the result after calling windowPosSum would be {4, 8, -3, 13, 9, 4}.

As another example, if we called windowPosSum with the array a = {1, -1, -1, 10, 5, -1}, and n = 2, we��d get {-1, -1, -1, 14, 4, -1}.

### ����
```java
public class sumNumbers {
    public static int[] windowPosSum(int[] a, int n) {
        /** ��һ�����鰴һ��������ӵõ����һ������*/
        int sum = 0;
        int[] b = new int[a.length];
        for(int i = 0;i<a.length;i++){
            if(a[i]>0){
                for(int j = i;j<i+n+1;j++){
                    if (j>=a.length){
                        break;
                    }else {
                        sum = sum + a[j];
                    }
                }
                b[i] = sum;
                sum = 0;
            }else{
                b[i]=a[i];
            }
        }
        return b;
    }

    public static void main(String[] args) {
        int[] a = {1, 2, -3, 4, 5, 4};
        int n = 3;
        int[] c = windowPosSum(a, n);

        // Should print 4, 8, -3, 13, 9, 4
        System.out.println(java.util.Arrays.toString(c));
    }
}
```
# С����
java����֪ʶҪ����

**ע�⣺  **
