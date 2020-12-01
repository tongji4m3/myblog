---
title: LeetCode刷题笔记94
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
  - Java
  - 二叉树
abbrlink: a41ffc13
date: 2020-05-15 00:00:00
---

> 题目出自LeetCode
>
>  [94. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述
给定一个二叉树，返回它的中序 遍历。

示例:
```
输入: [1,null,2,3]
   1
    \
     2
    /
   3

输出: [1,3,2]
```

# 思路

迭代:用栈的方式,思路和递归差不多。先往左走到底，不能走就回退一格，加入当前元素。然后继续查看当前元素的右节点。搞定完该节点，再回退一格。直到弄完根节点。

# 细节

# 代码

```java
//递归
public List<Integer> inorderTraversal(TreeNode root)
{
    List<Integer> result = new LinkedList<>();
    recursive(root, result);
    return result;
}

private void recursive(TreeNode node, List<Integer> result)
{
    if(node==null)
    {
        return;
    }
    recursive(node.left,result);
    result.add(node.val);
    recursive(node.right,result);
}
```



```java
//迭代
public List<Integer> inorderTraversal(TreeNode root)
{
    List<Integer> result = new LinkedList<>();
    Stack<TreeNode> stack = new Stack<>();
    TreeNode current = root;
    
    //current!=null 代表了还存在右节点
    //!stack.isEmpty() 代表了存在父节点
    //当然开始时只是看根节点
    while(current!=null || !stack.isEmpty())
    {
        while(current!=null)
        {
            stack.push(current);
            current = current.left;
        }
        current = stack.pop();
        result.add(current.val);
        current = current.right;
    }
    return result;
}
```





