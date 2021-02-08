---
title: LeetCode刷题笔记_208_实现 Trie (前缀树)
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: LeetCode刷题笔记
categories: LeetCode笔记
tags:
  - LeetCode
  - 字符串
  - 树
abbrlink: f5d941ba
date: 2020-06-14 00:00:00
---

> 题目出自LeetCode
>
> [208. 实现 Trie (前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述
```java
实现一个 Trie (前缀树)，包含 insert, search, 和 startsWith 这三个操作。

示例:

Trie trie = new Trie();

trie.insert("apple");
trie.search("apple");   // 返回 true
trie.search("app");     // 返回 false
trie.startsWith("app"); // 返回 true
trie.insert("app");   
trie.search("app");     // 返回 true
说明:

你可以假设所有的输入都是由小写字母 a-z 构成的。
保证所有输入均为非空字符串。
```

# 思路

使用`26叉树`的结构,每当有一个单词加进来,就顺着路径不断的初始化`Node`,并且在最后一个`Node`出赋值,代表单词的结束。

查找过程即根据单词每个字符对应的数组下标，不断在**单词搜索树中查询**，如果找到为空的`Node`，或者结尾处为-1，代表这个单词不存在。

查找前缀过程和查找过程一样，**只是他不要求前缀结尾部分的Node值为-1**

# 


# 代码

```java
public class Demo208
{
    private Node root;

    private class Node
    {
        int value;
        Node [] next;

        public Node()
        {
            this.value = -1;
            this.next = new Node[26];
        }
    }
    public Demo208()
    {
        root = new Node();
    }

    public void insert(String word)
    {
        Node temp = root;
        for (char ch : word.toCharArray())
        {
            int index = ch - 'a';
            if(temp.next[index]==null) temp.next[index] = new Node();
            temp = temp.next[index];
        }
        temp.value = 1;
    }

    public boolean search(String word)
    {
        Node temp = root;
        for (char ch : word.toCharArray())
        {
            int index = ch - 'a';
            if(temp.next[index]==null) return false;
            temp = temp.next[index];
        }
        return temp.value == 1;
    }

    public boolean startsWith(String prefix)
    {
        Node temp = root;
        for (char ch : prefix.toCharArray())
        {
            int index = ch - 'a';
            if(temp.next[index]==null) return false;
            temp = temp.next[index];
        }
        return true;
    }
}
```