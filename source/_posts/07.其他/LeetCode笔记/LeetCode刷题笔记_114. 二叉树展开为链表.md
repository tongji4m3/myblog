---
title: LeetCode刷题笔记114
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
  - 链表
abbrlink: 4c8e0e7
date: 2020-05-27 00:00:00
---

> 题目出自LeetCode
>
> [114. 二叉树展开为链表](https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/)
>
> 其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

给定一个二叉树，原地将它展开为一个单链表。


```
例如，给定二叉树

    1
   / \
  2   5
 / \   \
3   4   6
将其展开为：

1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6

```

# 思路

按照中序遍历的顺序构造成链表,并将之放在右子树的位置上

# 细节

需要原地展开

# 代码

```java
/**
 *
 * 该做法是不断将右子树放在左子树的最后一个节点上,再将左子树变为右子树
 * 更加直观,更加符合中左右的形式
 */
public void flatten(TreeNode root)
{
    while(root!=null)
    {
        //没有左子树,则直接到下一个右子树上,不需要继续考虑
        if(root.left!=null)
        {
            //找到左子树最右节点
            TreeNode temp = root.left;
            while(temp.right!=null)
            {
                temp = temp.right;
            }

            //将右子树放在左子树的最后一个节点上
            temp.right = root.right;

            //将左子树变为右子树
            root.right = root.left;
            root.left = null;
        }
        root = root.right;
    }
}
```

```java

    /**
     * 该方法是先把左子树放当前节点右边,当到最后一个左节点时,再放入右节点
     * 速度比较慢
     */
public void flatten(TreeNode root)
{
    Stack<TreeNode> stack = new Stack<>();
    while(root!=null)
    {
        //保存当前节点的右节点
        if(root.right!=null)
        {
            stack.push(root.right);
        }

        //将当前节点的左子树转移到右子树
        root.right = root.left;
        root.left = null;

        //说明往左遍历结束了
        if(root.right==null)
        {
            if(!stack.isEmpty())
            {
                root.right = stack.pop();
            }
            else
            {
                //说明左右子树都没了
                return;
            }
        }
        root = root.right;
    }
}
```


