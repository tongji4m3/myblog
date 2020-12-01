---
title: LeetCode刷题笔记105
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
  - 遍历
abbrlink: 6ad4e130
date: 2020-05-25 00:00:00
---

> 题目出自LeetCode
>
> [105. 从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

根据一棵树的前序遍历与中序遍历构造二叉树。

注意:
	你可以假设树中没有重复的元素。

```
例如，给出

前序遍历 preorder = [3,9,20,15,7]
中序遍历 inorder = [9,3,15,20,7]
返回如下的二叉树：

    3
   / \
  9  20
    /  \
   15   7
```

# 思路

对于前序与中序遍历的数组[lo,hi]:

+ 前序的根节点是lo,中序的根节点是i
+ 前序的左子树是[lo+1,i],右子树是[i+1,hi]
+ 中序的左子树是[lo,i-1],右子树是[i+1,hi]

由此,可以先构造根节点,然后根据前序中序的左右数组构造他的左右节点,一直不断递归下去...

# 细节

1. 注意几次递归后前序,中序数组可能不是上下对称的,所以他们索引index得区分为preIndex,inIndex
2. 用map存储可以加快速度

# 代码

```java
/**
 * look 用map存储加快速度
树中没有重复元素
用map存储inorder数组的值和对应索引
 方便找到根节点位置
 */
private Map<Integer, Integer> map = new HashMap<>();

public TreeNode buildTree(int[] preorder, int[] inorder)
{
    for (int i = 0; i < inorder.length; i++)
    {
        map.put(inorder[i], i);
    }
    return buildTree(preorder, 0, preorder.length - 1, inorder, 0, inorder.length - 1);
}

private TreeNode buildTree(int[] preorder, int preLo, int preHi, int[] inorder, int inLo, int inHi)
{
    if (preLo > preHi || inLo > inHi)
    {
        return null;
    }
    //找到根节点在中序遍历的索引位置
    int inIndex = map.get(preorder[preLo]);
    //look,i在经过几次之后,只是对应了inorder的i,但是对于preorder,应该只是一个偏移量
    //inIndex - inLo代表左子树的个数,preIndex则是前序遍历左子树的最后一个元素
    int preIndex = preLo + inIndex - inLo;
    TreeNode root = new TreeNode(preorder[preLo]);
    root.left = buildTree(preorder, preLo + 1, preIndex, inorder, inLo, inIndex - 1);
    root.right = buildTree(preorder, preIndex + 1, preHi, inorder, inIndex + 1, inHi);
    return root;
}
```


