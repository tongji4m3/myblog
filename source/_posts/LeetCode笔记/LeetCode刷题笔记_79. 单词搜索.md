---
title: LeetCode刷题笔记79
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
  - 深搜
abbrlink: 442dad20
date: 2020-05-11 00:00:00
---

> 题目出自LeetCode
>
> [79. 单词搜索](https://leetcode-cn.com/problems/word-search/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述
给定一个二维网格和一个单词，找出该单词是否存在于网格中。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

 

示例:
```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
给定 word = "ABCCED", 返回 true
给定 word = "SEE", 返回 true
给定 word = "ABCB", 返回 false
```



提示：
```
board 和 word 中只包含大写和小写英文字母。
1 <= board.length <= 200
1 <= board[i].length <= 200
1 <= word.length <= 10^3
```

# 思路

深度优先搜索,在同一个搜索中,将搜索过的改变为*或其他标识,搜索后再恢复

```java
for i in M:
	for j in N:
		if dfs(i,j,0) return true; //如果找到了就直接结束,找不到就继续找


dfs(int i,int j,int index)
{
    if(board[i][j]!=word[index]) return false;
    if(index==word.length-1) return true;
    
    temp=board[i][j];
    board[i][j]='*';//标记为已访问
    
    如果符合边界条件,dfs(他的上下左右,index+1);
    
    board[i][j]=temp;//这次深搜结束,恢复
}
```



# 细节

1. 找到了可以直接返回,不进入二维数组,找不到则要继续,所以注意条件
2. dfs里,return的条件是四个方向都找不到才返回false

# 代码

```java
public boolean exist(char[][] board, String word)
{
    if (board.length == 0)
    {
        return false;
    }
    int m = board.length, n = board[0].length;

    for (int i = 0; i < m; i++)
    {
        for (int j = 0; j < n; j++)
        {
            if (dfs(board, word, i, j, 0))
            {
                return true;
            }
        }
    }
    return false;
}

private boolean dfs(char[][] board, String word, int i, int j, int index)
{
    if (board[i][j] != word.charAt(index))
    {
        return false;
    }
    if (index == word.length() - 1)
    {
        return true;
    }

    char temp = board[i][j];
    //标记为已访问
    board[i][j] = '*';

    boolean result = false;

    if (i - 1 >= 0)
    {
        result = dfs(board, word, i - 1, j, index + 1);
    }
    if (i + 1 < board.length)
    {
        result = result || dfs(board, word, i + 1, j, index + 1);
    }
    if (j - 1 >= 0)
    {
        result = result || dfs(board, word, i, j - 1, index + 1);
    }
    if (j + 1 < board[0].length)
    {
        result = result || dfs(board, word, i, j + 1, index + 1);
    }
    //这次深搜结束,恢复
    board[i][j] = temp;
    return result;
}
```




