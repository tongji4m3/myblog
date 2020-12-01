---
title: LeetCode刷题笔记101
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
abbrlink: 6db92529
date: 2020-05-21 00:00:00
---

> 题目出自LeetCode
>
>  [101. 对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

给定一个二叉树，检查它是否是镜像对称的。


```
例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

    1
   / \
  2   2
 / \ / \
3  4 4  3


但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    1
   / \
  2   2
   \   \
   3    3
```

# 思路

递归,每次分为两次递归,判断最外层的两个节点,最内侧两节点是否相等

# 细节

注意节点为空的情况


# 代码
```java
public boolean isSymmetric(TreeNode root)
{
    return recursive(root, root);
}

private boolean recursive(TreeNode left,TreeNode right)
{
    if(left==null && right==null)
    {
        return true;
    }
    else if(left==null || right==null)
    {
        return false;
    }
    else
    {
        return left.val == right.val && recursive(left.left, right.right) && recursive(left.right, right.left);
    }
}
```
