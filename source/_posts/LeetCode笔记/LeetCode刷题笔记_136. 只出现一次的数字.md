---
title: LeetCode刷题笔记136
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: true
summary: LeetCode刷题笔记
categories: LeetCode笔记
tags:
  - LeetCode
  - 数组
  - 异或
abbrlink: d8f0e349
date: 2020-05-31 00:00:00
---

> 题目出自LeetCode
>
> [136. 只出现一次的数字](https://leetcode-cn.com/problems/single-number/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。找出那个只出现了一次的元素。

说明：

你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

示例 1:
```
输入: [2,2,1]
输出: 1
```
示例 2:
```
输入: [4,1,2,1,2]
输出: 4
```


# 思路
因为一个数对同一个数异或两次会得到原本的结果，所以对数组循环遍历一遍，对每一个数进行异或，就会得到单独剩下的那个数。


# 代码



```java
public int singleNumber(int[] nums)
{
    if(nums.length==0) throw new IllegalArgumentException();
    int result = nums[0];
    for (int i = 1; i < nums.length; i++) result ^= nums[i];
    return result;
}
```