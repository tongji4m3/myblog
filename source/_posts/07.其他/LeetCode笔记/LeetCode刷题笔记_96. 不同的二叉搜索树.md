---
title: LeetCode刷题笔记96
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
  - 二叉树
  - 动态规划
abbrlink: 4a119d3f
date: 2020-05-17 00:00:00
---

> 题目出自LeetCode
>
> [96. 不同的二叉搜索树](https://leetcode-cn.com/problems/unique-binary-search-trees/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

给定一个整数 n，求以 1 ... n 为节点组成的二叉搜索树有多少种？

示例:
```
输入: 3
输出: 5
解释:
给定 n = 3, 一共有 5 种不同结构的二叉搜索树:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3

```

# 思路

```
动态规划:

dp[i]代表n=i时组成的二叉搜索树的种类数量

初始化: dp[0]=1,dp[1]=1

递推方程:
for j in [1,i]:
		dp[i]+=dp[j-1]*dp[i-j]

返回:dp[n]
```



```
for i in [2,n]:
	for j in [1,i]:
		dp[i]+=dp[j-1]*dp[i-j]
```



# 细节

注意i从2开始


# 代码

```java
public int numTrees(int n)
{
    if(n<1)
    {
        throw new IllegalArgumentException();
    }

    int[] dp = new int[n + 1];
    //dp[0]=1也可以代表的是,左边(右边)为空的情况有一种
    dp[0] = 1;
    dp[1] = 1;
    //look,i要从2开始,1的话是初始值,如果从1开始,则dp[1]=2
    for (int i = 2; i <= n; i++)
    {
        for (int j = 1; j <= i; j++)
        {
            dp[i] += dp[j - 1] * dp[i - j];
        }
    }
    return dp[n];
}
```