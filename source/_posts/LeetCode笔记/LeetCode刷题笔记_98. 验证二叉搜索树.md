---
title: LeetCode刷题笔记98
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
abbrlink: ada9b038
date: 2020-05-19 00:00:00
---

> 题目出自LeetCode
>
> [98. 验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

节点的左子树只包含小于当前节点的数。
		节点的右子树只包含大于当前节点的数。
		所有左子树和右子树自身必须也是二叉搜索树。
示例 1:

```
输入:
    2
   / \
  1   3
输出: true
```




示例 2:
```
输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。
```

# 思路

中序遍历,如果后面的节点小于等于前面的节点,就不是二叉搜索树

# 细节

使用isFirst避免下面特殊情况出现错误:

如果最左边的正好是Integer.MIN_VALUE或者有两个Integer.MIN_VALUE

# 代码

```java
public boolean isValidBST(TreeNode root)
{
    Stack<TreeNode> stack=new Stack<>();
    TreeNode temp = root;
    boolean isFirst = true;
    int pre=0;
    while(temp!=null || !stack.isEmpty())
    {
        while(temp!=null)
        {
            stack.push(temp);
            temp = temp.left;
        }
        temp = stack.pop();
        if(isFirst)
        {
            pre = temp.val;
            isFirst = false;
        }
        else if(temp.val<=pre)
        {
            return false;
        }
        pre = temp.val;
        temp = temp.right;
    }
    return true;
}
```