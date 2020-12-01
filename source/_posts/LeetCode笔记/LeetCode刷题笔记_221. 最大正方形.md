---
title: LeetCode刷题笔记221._最大正方形
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
  - 动态规划
  - 二维数组
abbrlink: 7b573481
date: 2020-10-08 00:00:00
---

> 题目出自LeetCode
>
> [221. 最大正方形](https://leetcode-cn.com/problems/maximal-square/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述
在一个由 0 和 1 组成的二维矩阵内，找到只包含 1 的最大正方形，并返回其面积。
```java
示例:

输入: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

输出: 4
```


# 思路
1. 采用动态规划的思想,`dp[i][j]`代表最大的正方形边长,从左到右,从上到下进行扫描
2. 或者可以采用处理这种问题的通用方法,即定义`height,left,right`数组,逐层扫描,逐层计算result

# 细节

## 方法1

1. 初始化为:`int[][] dp = new int[m + 1][n + 1];`,这样可以不需要再处理初始的边界问题
2. 动态规划递推公式为:` dp[i][j] = Math.min(dp[i - 1][j], Math.min(dp[i][j - 1], dp[i - 1][j - 1])) + 1;`,因为是正方形,所以需要他左,上,左上三个角都有才能构成更大的正方形。

## 方法2

1. 在对每一层处理时，首先要考虑他们和上一层的关系
2. `left`数组是从左往右处理，`right`数组是从右往左处理
3. 小心处理当`matrix[i][j]==0`的情况，要考虑对下层的影响。例如当`matrix[i][j]==0`，需要让`left[j] = 0`，以便下层缩小范围。



# 代码

## 方法1

```java
public int maximalSquare(char[][] matrix)
{
    if (matrix.length == 0) return 0;
    int m = matrix.length, n = matrix[0].length;
    int result = 0;
    int[][] dp = new int[m + 1][n + 1];//dp[i][j]代表最大的正方形边长
    for (int i = 1; i <= m; i++)
    {
        for (int j = 1; j <= n; j++)
        {
            if(matrix[i-1][j-1]=='1')
            {
                dp[i][j] = Math.min(dp[i - 1][j], Math.min(dp[i][j - 1], dp[i - 1][j - 1])) + 1;
                result = Math.max(result, dp[i][j] * dp[i][j]);
            }
        }
    }

    return result;
}
```

## 方法2

```java
public int maximalSquare(char[][] matrix)
{
    if (matrix.length == 0) return 0;
    int m = matrix.length, n = matrix[0].length;
    int result = 0;
    int[] height = new int[n];
    int[] left = new int[n];
    int[] right = new int[n];

    for (int i = 0; i < n; i++) right[i] = n; //look

    for (int i = 0; i < m; i++)
    {
        //对height赋值
        for (int j = 0; j < n; j++)
        {
            if (matrix[i][j] == '1') height[j] += 1;
            else height[j] = 0;
        }

        //对left赋值
        int leftIndex = 0;
        for (int j = 0; j < n; j++)
        {
            if (matrix[i][j] == '1')
            {
                //继承上一个的
                left[j] = Math.max(leftIndex,left[j]);
            }
            else
            {
                left[j] = 0;//考虑下面继承他的范围,就要放宽
                leftIndex = j + 1;
            }
        }

        //right赋值
        int rightIndex = n;
        for(int j = n-1; j >= 0; j--)
        {
            if (matrix[i][j] == '1')
            {
                right[j] = Math.min(rightIndex,right[j]);
            }
            else
            {
                right[j] = n;
                rightIndex = j;
            }
        }

        //计算正方形
        for (int j = 0; j < n; j++)
        {
            int value = Math.min(right[j] - left[j], height[j]);
            result = Math.max(result, value * value);
        }
    }

    return result;
}
```