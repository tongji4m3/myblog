---
title: LeetCode刷题笔记78
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
  - 解空间树
abbrlink: 332a9db6
date: 2020-05-09 00:00:00
---

> 题目出自LeetCode
>
> [78. 子集](https://leetcode-cn.com/problems/subsets/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)

# 描述

给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

示例:
```
输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

# 思路

画出解空间树,相当于把解空间树所有的元素都加入到了集合中(去掉重复的集合)

```java
boolean [] marked;
recursive(0);

recursive(int height)
{
    result.add(temp);
    if(height==N) return;
    for i in N
    {
        if(!marked[i])
        {
            temp.add(nums[i]);
            marked[i]=true;
            recursive(height+1);
            marked[i]=false;
            temp.remove(nums[i]);          
              
        }
    }
}
```





# 细节

1. 注意还要去掉重复的集合,所以可以直接采用偏序简化代码


# 代码

```java
private List<Integer> temp = new LinkedList<>();
private List<List<Integer>> result = new LinkedList<>();

public List<List<Integer>> subsets(int[] nums)
{
    recursive(nums,0);
    return result;
}

public void recursive(int[] nums,int start)
{
    result.add(new LinkedList<>(temp));

    for (int i = start; i < nums.length; i++)
    {
        temp.add(nums[i]);
        recursive(nums,i+1);
        temp.remove(temp.size()-1);
    }
}
```

```java
//循环
//本质上就是模拟一个个元素不断加入集合的过程
public List<List<Integer>> subsets(int[] nums)
{
    List<List<Integer>> result = new LinkedList<>();
    result.add(new LinkedList<>());//刚开始为空集

    for (int i = 0; i < nums.length; i++)
    {
        //加入元素nums[i]所得到的额外的list
        List<List<Integer>> list = new LinkedList<>();
        for (List<Integer> e : result)//就是通过原本的每个集合都加入该元素
        {
            List<Integer> temp = new LinkedList<>(e);
            temp.add(nums[i]);
            list.add(temp);
        }
        result.addAll(list);
    }
    return result;
}
```



# 复杂度分析
## 时间复杂度

$O(1)$

## 空间复杂度

$O(1)$