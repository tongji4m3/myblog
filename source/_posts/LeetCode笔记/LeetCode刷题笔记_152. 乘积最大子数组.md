---
title: LeetCode刷题笔记152
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
  - 数组
  - 动态规划
abbrlink: 89c780d6
date: 2020-06-10 00:00:00
---

> 题目出自LeetCode
>
> [152. 乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/)
>
> 
>
> 其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述
给你一个整数数组 nums ，请你找出数组中乘积最大的连续子数组（该子数组中至少包含一个数字），并返回该子数组所对应的乘积。

 

示例 1:
```
输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
```
示例 2:
```
输入: [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。
```

# 思路

```
dp[i]代表连续子数组乘到i的最大值
min[i]代表连续子数组乘到i的最小值

int result=0;
dp[0]=nums[0]
min[0]=nums[0]
for i in N:
    if(nums[i]>0) 
    {
        dp[i]=nums[i]*max(1,dp[i-1]);//适当时候抛弃前面的
		min[i]=min(min[i-1],1)*nums[i];
    }
    else
    {
        dp[i]=nums[i]*min(min[i-1],1);//适当时候抛弃前面的
        min[i]=max(dp[i-1],1)*nums[i];
    }
    result=max(dp[i],result)

```

```
//简化后的思路:
		for (int i = 1; i < N; i++)
        {
            int temp = max;
            max = Math.max(max * nums[i], Math.max(nums[i] * min, nums[i]));
            min = Math.min(min * nums[i], Math.min(temp * nums[i], nums[i]));
            result = Math.max(max, result);
        }
```



# 细节

压缩空间后,记得处理好他们的依赖关系

# 代码

```java
//经典动态规划
public int maxProduct(int[] nums)
{
    int N = nums.length;
    if (N == 0) return 0;

    int[] max = new int[N];
    int[] min = new int[N];

    int result = nums[0];//注意初始值
    max[0] = nums[0];
    min[0] = nums[0];

    for (int i = 1; i < N; i++)
    {
        if (nums[i] > 0)
        {
            max[i] = nums[i] * Math.max(1, max[i - 1]);//适当时候抛弃前面的
            min[i] = Math.min(min[i - 1], 1) * nums[i];
        }
        else
        {
            max[i] = nums[i] * Math.min(min[i - 1], 1);//适当时候抛弃前面的
            min[i] = Math.max(max[i - 1], 1) * nums[i];
        }
        result = Math.max(max[i], result);
    }
    return result;
}
```

```java
//压缩空间
public int maxProduct(int[] nums)
{
    int N = nums.length;
    if(N==0) return 0;
    int max = nums[0], min = nums[0], result = nums[0];

    for (int i = 1; i < N; i++)
    {
        if (nums[i] > 0)
        {
            max = nums[i] * Math.max(1, max);//适当时候抛弃前面的
            min = Math.min(min, 1) * nums[i];
        }
        else
        {
            int temp=max;
            max = nums[i] * Math.min(min, 1);//适当时候抛弃前面的
            //look,这里min依赖与max[i-1]
            min = Math.max(temp, 1) * nums[i];
        }
    }
    return result;
}
```

```java
    //压缩空间后进一步简化版本
    public int maxProduct(int[] nums)
    {
        int N = nums.length;
        if (N == 0) return 0;
        int max = nums[0], min = nums[0], result = nums[0];

        for (int i = 1; i < N; i++)
        {
            int temp = max;
            max = Math.max(max * nums[i], Math.max(nums[i] * min, nums[i]));
            min = Math.min(min * nums[i], Math.min(temp * nums[i], nums[i]));
            result = Math.max(max, result);
        }
        return result;
    }
```