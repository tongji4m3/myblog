---
title: LeetCode刷题笔记104
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
  - 递归
abbrlink: 1dd3d1a6
date: 2020-05-24 00:00:00
---

> 题目出自LeetCode
>
>  [104. 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。
```
示例：
给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7
   
返回它的最大深度 3 。
```




# 代码
```java
public int maxDepth(TreeNode root)
{
	if(root==null) return 0;
	return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1;
}
```

