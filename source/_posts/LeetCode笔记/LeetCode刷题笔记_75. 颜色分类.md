---
title: LeetCode刷题笔记75
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
  - 快排
abbrlink: 4d9be10b
date: 2020-05-05 00:00:00
---

> 题目出自LeetCode
>
> [75. 颜色分类](https://leetcode-cn.com/problems/sort-colors/)

>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)

# 描述

给定一个包含红色、白色和蓝色，一共 n 个元素的数组，原地对它们进行排序，使得相同颜色的元素相邻，并按照红色、白色、蓝色顺序排列。

此题中，我们使用整数 0、 1 和 2 分别表示红色、白色和蓝色。

注意:
不能使用代码库中的排序函数来解决这道题。

示例:

```
输入: [2,0,2,1,1,0]
输出: [0,0,1,1,2,2]
```


进阶：

一个直观的解决方案是使用计数排序的两趟扫描算法。
首先，迭代计算出0、1 和 2 元素的个数，然后按照0、1、2的排序，重写当前数组。
你能想出一个仅使用常数空间的一趟扫描算法吗？

# 思路

采用快排的partition思想,在数组首尾定义指针,lo标识0的结束(保证lo-1处一定为0),hi标识2的开始(保证hi+1处一定为2).再用指针i来遍历数组

一个比较好的测试用例`2 0 1 0 1 2`

# 代码
```java
public void sortColors(int[] nums)
{
    int lo=0,hi=nums.length-1;
    int i=0;
    while(i<=hi)
    {
        if(nums[i]==0)
        {
            //exch(nums,i++,lo++); 由于特殊性,化简
            nums[i++] = nums[lo];
            nums[lo++] = 0;
        }
        else if(nums[i]==1)
        {
            ++i;
        }
        else
        {
            //                exch(nums,i,hi--);
            nums[i] = nums[hi];
            nums[hi--] = 2;
        }

    }
}
```

