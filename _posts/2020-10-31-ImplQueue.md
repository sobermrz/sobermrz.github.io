---
layout: post # 使用的布局（不需要改）
title: Implement of Queue # 标题
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

public class MyQueue<T> {
		//initialize
		T[] arr = null;

		public MyQueue(){
			arr = (T[])new Object[0];
		}

		// ADD/OFFER Func
		public void add(T element) {
			//create a new array 1 longer than the original one
			T[] newArr = (T[])new Object[arr.length + 1];

			//copy all element from arr to newArr
			for(int i = 0; i < arr.length; i++) {
				newArr[i] = arr[i];
			}

			//put the new element into the end of newArr
			newArr[newArr.length - 1] = element;

			//copy newArr to arr
			arr = newArr;
		}

		// POLL/Remove Func
		public T poll() {
			//check first
			if(arr.length == 0) {
				throw new ArrayIndexOutOfBoundsException();
			}

			//create a newArr 1 shorter than arr
			T[] newArr = (T[])new Object[arr.length - 1];

			//copy all element from arr to the newArr(except the first one)
			for(int i = 0; i < newArr.length; i++) {
				newArr[i] = arr[i + 1];
			}

			//get the last element in arr
			T ele = arr[0];

			//copy newArr to arr
			arr = newArr;

			//return the last element
			return ele;
		}

		// PEEL/ELEMENT Func
		public T peek() {
			//check first
			if(arr.length == 0) {
				throw new ArrayIndexOutOfBoundsException();
			}
			//return the last element in the array
			return arr[0];
		}

		//ISEMPTY Func
		public boolean isEmpty() {
			return arr.length == 0;
		}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		MyQueue ms = new MyQueue();

		// 进队
		ms.add(99);
		ms.add(98);
		ms.add(97);
		ms.add(96);
		ms.add("a");
		ms.add("b");
		ms.add("c");

		// 出队
		System.out.println(ms.poll());
		System.out.println(ms.poll());
		System.out.println(ms.poll());
		System.out.println(ms.poll());
		System.out.println(ms.poll());
		System.out.println(ms.poll());

		System.out.println(ms.isEmpty());
	}

}

```
