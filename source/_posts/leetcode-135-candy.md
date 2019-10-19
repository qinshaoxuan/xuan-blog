---
title: LeetCode 135 Candy
tags:
  - 贪心
url: 769.html
id: 769
categories:
  - LeetCode
date: 2015-11-14 15:13:37
mathjax: true
cover: /img/48889436_p0.jpg
---


> 题目链接：[Candy](https://leetcode.com/problems/candy/) 
> 题意：N个孩子排成一排，每个孩子有个rating值，现在给每个孩子发糖果，要求：
> 
> *   每人至少一个
> *   rating值比相邻孩子高的人得的糖果数要比相邻的多
> 
> 求糖果总数最少是多少？

贪心，每人尽量发最少的糖。 
若$L_i$表示第i个数左边相邻非递减区间去重后的长度 $R_i$表示第i个数右边相邻非递增区间去重后的长度 那么第i个孩子得到的糖果数为$max(L_i,R_i)$ 
时间复杂度$O(n)$  

```java
public class Solution {
    public int candy(int[] ratings) {
		int[] l = new int[ratings.length];
		int[] r = new int[ratings.length];
		int ans = 0;

		for (int i = 1; i < ratings.length; i++) {
			if (ratings[i] > ratings[i - 1])
				l[i] = l[i - 1] + 1;
			else
				l[i] = 0;
		}
		for (int i = ratings.length - 2; i >= 0; i--) {
			if (ratings[i] > ratings[i + 1])
				r[i] = r[i + 1] + 1;
			else
				r[i] = 0;
		}

		for (int i = 0; i < ratings.length; i++)
			ans += Math.max(l[i], r[i]) + 1;

		return ans;
	}
}
```
