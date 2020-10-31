---
layout: post # 使用的布局（不需要改）
title: Implement of List # 标题
subtitle: #副标题
date: 2020-10-30 # 时间
author: Ruizhi Ma # 作者
header-img: #这篇文章标题背景图片
catalog: true # 是否归档
tags: #标签
  - Data Structure
---

```java
package test;

public class MyList {
	Node head = null;

	//initialize the node
	class Node{
		Node next = null;
		int data;

		public Node(int data) {
			this.data = data;
		}
	}

	//add node at the end of the list
	public void addNode(int val) {
		Node node = new Node(val);

		//if the list has nothing, then let node to be the head
		if(head == null) {
			head = node;
			return;
		}

		Node temp = head;

		//move to the end of the list
		while(temp.next != null) {
			temp = temp.next;
		}

		temp.next = node;
	}

	//calculate the length of the list
	public int length() {
		int len = 0;
		Node temp = head;

		while(temp != null) {
			temp = temp.next;
			len++;
		}

		return len;
	}

	//print the list
	public void printList() {
		Node temp = head;

		while(temp != null) {
			System.out.print(temp.data + ",");
			temp = temp.next;
		}
	}

	//delete node according to the index
	public void deleteNode(int index) {
		//check
		if(index < 1 || index >= length()) System.out.println("Error: Out of bound!");

		if(index == 1) {
			head =  null;
			return;
		}

		Node pre = head;
		Node cur = pre.next;

		int i = 1;

		while(cur != null) {
			if(i == index) {
				pre.next = cur.next;
			}

			pre = cur;
			cur = cur.next;
			i++;
		}


	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		MyList list = new MyList();
        list.addNode(5);
        list.addNode(3);
        list.addNode(1);
        list.addNode(2);
        list.addNode(55);
        list.addNode(36);
        System.out.println("linkLength:" + list.length());
        System.out.println("head.data:" + list.head.data);
        list.printList();
        System.out.println();
        list.deleteNode(4);
        System.out.println("After deleteNode(4):");
        list.printList();
	}

}


```
