---
title: LeetCode刷题笔记102
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
  - 层次遍历
abbrlink: f4b07493
date: 2020-05-22 00:00:00
---

> 题目出自LeetCode
>
> [102. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

 ```

示例：
二叉树：[3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]

 ```
# 思路

递归的思路：从根节点，高度为0处开始递归。首次进入某层时,就开辟新的空间,随后进入相同的层则直接根据他所在的高度加入即可




# 代码

```java
private List<List<Integer>> result = new LinkedList<>();

public List<List<Integer>> levelOrder(TreeNode root)
{
    recursive(root, 0);
    return result;
}

private void recursive(TreeNode node, int height)
{
    if(node==null)
    {
        return;
    }
    //最多就是等于,不会大于,因为每层不满足都会构建
    if(height==result.size())
    {
        result.add(new LinkedList<>());
    }
    result.get(height).add(node.val);

    recursive(node.left,height+1);
    recursive(node.right,height+1);
}
```