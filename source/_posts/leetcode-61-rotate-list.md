---
title: LeetCode 61 Rotate List
url: 1409.html
id: 1409
categories:
  - LeetCode
date: 2016-07-22 23:20:16
tags: 链表
cover: /img/1409.jpg
---


> 题目链接：[Rotate List](https://leetcode.com/problems/rotate-list/) 
> 题意：将链表向右滚动，超出末尾的链接在头部

依旧是考验细节的题，第一次遍历的时候记录下长度，第二次历遍根据移动的距离得到移动后的链表的头结点和尾结点，再处理下引用关系即可。

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode rotateRight(ListNode head, int k) {
		if (head == null || k == 0)
			return head;
		int len = 1;
		ListNode x = head;

		while (x.next != null) {
			x = x.next;
			len++;
		}
		x.next = head;
		k = k % len;
		while (k++ < len)
			x = x.next;

		ListNode last = x;
		ListNode first = x.next;

		last.next = null;
		return first;
	}
}
```