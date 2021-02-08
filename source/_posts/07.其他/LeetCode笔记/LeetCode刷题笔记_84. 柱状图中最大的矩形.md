---
title: LeetCode刷题笔记84
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
  - 栈
  - 数组
abbrlink: bd04cd52
date: 2020-05-13 00:00:00
---

> 题目出自LeetCode
>
> [84. 柱状图中最大的矩形](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

给定 *n* 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

**示例:**

```
输入: [2,1,5,6,2,3]
输出: 10
```

# 思路

整体思路是最大矩形是遍历一遍数组，分别查看以索引i为高度所形成的矩形，取他们的最大值

维护一个递增序列。当遇到一个递减的元素，前面比他高的元素所能形成的矩形已经确定了，即可计算出来。然后继续，直到遍历完数组，此时有一个递增序列。

对于这个序列中的某个元素nums[i],他的右边界是数组最后一个元素，左边界是下一个栈元素+1（画图出来考虑）

[liweiwei1419的解法](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/solution/bao-li-jie-fa-zhan-by-liweiwei1419/)

```java
Stack<Integer> stack;//递增序列 存储的是索引下标 
for i in N
{
	//nums[stack.top()]=nums[i]的要留下,因为前面的元素还可以继续扩展
    while(!stack.isEmpty() && nums[stack.top()]>nums[i])
	{
		//这里计算的是以弹出那个元素为高度的最大矩形
		int index=stack.pop();
		result=max(result,(i-index)*nums[index]);
	}
	stack.push(i);//此时为递增序列
}
//对递增序列进行计算
//这些元素每一个都可以扩展到数组尽头
while(!stack.isEmpty())
{
	//范围是[ stack.top()+1 , N-1 ]
	int index=stack.pop();
	result=max(result,(N-stack.top()-1)*nums[index]);
}
```



# 细节

1. stack底部用一个-1标识，不然计算索引为0的元素的左边界有问题
2. 注意左边界的计算不能直接为索引i（因为要注意左边比他高的被忽略而不在栈中的元素）
3. 注意计算的都是以该索引位置的值为高，他左右两边能扩展的最大距离为宽


# 代码

```java
public int largestRectangleArea(int[] heights)
{
    //递增序列 存储的是索引下标
    Stack<Integer> stack = new Stack<>();
    int result = 0;
    int n = heights.length;
    //防止最左边元素计算不了面积
    stack.push(-1);
    for (int i = 0; i < n; i++)
    {
        //heights[stack.top()]=heights[i]的要留下,因为前面的元素还可以继续扩展
        while (stack.peek() != -1 && heights[stack.peek()] > heights[i])
        {
            //这里计算的是以弹出那个元素为高度的最大矩形
            int index = stack.pop();
            //look 这里也要按照下面的思路,即该元素的左边界是stack.top()+1 而不能仅仅是(i - index) * heights[index]
            result = Math.max(result, (i - stack.peek() - 1) * heights[index]);
        }
        //此时为递增序列
        stack.push(i);
    }
    //对递增序列进行计算
    //这些元素每一个都可以扩展到数组尽头
    while (stack.peek() != -1)
    {
        //范围是[ stack.top()+1 , N-1 ]
        int index = stack.pop();
        result = Math.max(result, (n - stack.peek() - 1) * heights[index]);
    }
    return result;
}
```



# 复杂度分析
## 时间复杂度

$O(N)$

## 空间复杂度

$O(N)$