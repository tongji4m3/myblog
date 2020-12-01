---
title: LeetCode刷题笔记121
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
  - 数组
  - 动态规划
abbrlink: 5f8f47ab
date: 2020-05-29 00:00:00
---

> 题目出自LeetCode
>
> [121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票一次），设计一个算法来计算你所能获取的最大利润。

注意：你不能在买入股票前卖出股票。

 

示例 1:
```
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格；同时，你不能在买入前卖出股票。
```
示例 2:
```
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

# 思路





```java
动态规划:

sell[i]:代表第i天卖出得到的最大利润

buy[i]:代表第i天买入的最大利润

sell[i] = max(0,price[i] - buy[i-1])

buy[i] = max(-price[i],buy[i-1])

初始化:buy[0]=-price[0],sell[0]=0

结果:result=max(result,sell[i])
```



# 细节

都可以节约空间,减少一个维度


# 代码

```java
//无化简的动态规划
public int maxProfit(int[] prices)
{
    int N = prices.length;
    if (N == 0)
    {
        return 0;
    }
    int[] buy = new int[N];
    int[] sell = new int[N];
    int result = 0;

    buy[0] = -prices[0];
    sell[0] = 0;

    for (int i = 1; i < N; i++)
    {
        buy[i] = Math.max(-prices[i], buy[i - 1]);
        //look,是+,不是-,因为buy[i]是负数
        sell[i] = Math.max(0, prices[i] + buy[i - 1]);
        result = Math.max(result, sell[i]);
    }
    return result;
}

//节约空间
public int maxProfit(int[] prices)
{
    int N = prices.length;
    if (N == 0) return 0;
    int buy=-prices[0],sell=0,result = 0;
    for (int i = 1; i < N; i++)
    {
        sell = Math.max(0, prices[i] + buy);
        buy = Math.max(-prices[i], buy);
        result = Math.max(result, sell);
    }
    return result;
}
```

