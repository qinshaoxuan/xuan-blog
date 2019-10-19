---
title: LeetCode 33 Search in Rotated Sorted Array
tags:
  - 二分
url: 730.html
id: 730
categories:
  - LeetCode
date: 2015-11-07 20:17:34
cover: /img/39759178_p0.png
---


> 题目链接：[Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) 
> 题意：给一个数组nums，这个数组是由一个另一个排好序的数组从某个位置截断，前半部分接在后半部分后面形成的。先给一个数target，查找它在数组nums中的位置。 0 1 2 4 5 6 7可以形成nums数组4 5 6 7 0 1 2

可以用二分查找。 将[L,R]分为[L,mid]和[mid,R]，那么这两个区间一定有一个是有序的 假设target在数组nums中，那么可以通过判断target是否在有序区间中来确定它是在哪一半
时间复杂度$O(log(n))$  

```java
public class Solution {
    public int search(int[] nums, int target) {
		int l = 0, r = nums.length - 1, mid;
		while (l <= r) {
			mid = (l + r) >> 1;
			if (nums[mid] == target)
				return mid;
			if ((nums[l] <= nums[mid] && (nums[l] <= target && target <= nums[mid]))
					|| (nums[l] > nums[mid] && !(nums[mid] <= target && target <= nums[r]))) {
				r = mid - 1;
			} else {
				l = mid + 1;
			}
		}
		return -1;
	}
}
```
