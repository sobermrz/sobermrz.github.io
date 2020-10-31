---
layout: post # 使用的布局（不需要改）
title: Implement of Stack # 标题
subtitle: #副标题
date: 2020-10-31 # 时间
author: Ruizhi Ma # 作者
header-img: #这篇文章标题背景图片
catalog: true # 是否归档
tags: #标签
  - Data Structure
---

```java
package test;

public class MyStack<T> {
	//initialize
	T[] arr = null;

	public MyStack(){
		arr = (T[])new Object[0];
	}

	//PUSH
	public void push(T element) {
		//create a new array 1 longer than the original one
		T[] newArr = (T[])new Object[arr.length + 1];

		//copy all element from arr to newArr
		for(int i = 0; i < arr.length; i++) {
			newArr[i] = arr[i];
		}

		//put the new element into the newArr
		newArr[newArr.length - 1] = element;

		//copy newArr to arr
		arr = newArr;
	}

	public T pop() {
		//check first
		if(arr.length == 0) {
			throw new ArrayIndexOutOfBoundsException();
		}

		//create a newArr 1 shorter than arr
		T[] newArr = (T[])new Object[arr.length - 1];

		//copy all element from arr to the newArr(except the last one)
		for(int i = 0; i < newArr.length; i++) {
			newArr[i] = arr[i];
		}

		//get the last element in arr
		T ele = arr[arr.length - 1];

		//copy newArr to arr
		arr = newArr;

		//return the last element
		return ele;
	}

	public T peek() {
		//check first
		if(arr.length == 0) {
			throw new ArrayIndexOutOfBoundsException();
		}
		//return the last element in the array
		return arr[arr.length - 1];
	}

	public boolean isEmpty() {
		return arr.length == 0;
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		// Create a stack
		MyStack ms = new MyStack();

		// PUSH func
		ms.push(100);
		ms.push(99);
		ms.push(98);
		ms.push(97);
		ms.push("a");
		ms.push("b");
		ms.push("c");

		// POP func
		System.out.println(ms.pop());
		System.out.println(ms.pop());
		System.out.println(ms.pop());
		System.out.println(ms.pop());
		System.out.println(ms.pop());
		System.out.println(ms.pop());

		System.out.println("----------------");

		// Peek func
		System.out.println(ms.peek());

		System.out.println("----------------");

		// ISEMPTY func
		System.out.println(ms.isEmpty());
	}

}

```
