---
title: LeetCode刷题笔记_207_课程表
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: 'LeetCode刷题笔记,主要是图论,拓扑排序判断是否有环等相关知识。'
categories: LeetCode笔记
tags:
  - LeetCode
  - 图
  - dfs
abbrlink: 5e9da042
date: 2020-10-03 00:00:00
---

> 题目出自LeetCode
>
> [207. 课程表](https://leetcode-cn.com/problems/course-schedule/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

你这个学期必须选修 `numCourse` 门课程，记为 0 到`numCourse-1` 。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们：`[0,1]`

给定课程总量以及它们的先决条件，请你判断是否可能完成所有课程的学习？

 

示例 1:

```java

输入: 2, [[1,0]] 
输出: true
解释: 总共有 2 门课程。学习课程 1 之前，你需要完成课程 0。所以这是可能的。
```
示例 2:
```java
输入: 2, [[1,0],[0,1]]
输出: false
解释: 总共有 2 门课程。学习课程 1 之前，你需要先完成课程 0；并且学习课程 0 之前，你还应先完成课程 1。这是不可能的。
```

提示：

```java
输入的先决条件是由 边缘列表 表示的图形，而不是 邻接矩阵 。详情请参见图的表示法。
你可以假定输入的先决条件中没有重复的边。
1 <= numCourses <= 10^5
```







# 思路

该题为拓扑排序相关问题。

首先先**构造图**。可以先将课程转为图的顶点，再为课程关系转为有向图中的边。

随后判断图是否是**无环图**,无环图则代表这样的课程顺序符合规范。具体做法为用`dfs`进行遍历，且每次遍历时维护一个cycle以作为每次有环的判断。

# 细节

维护一个全局变量`hasCycle`可以在有环时直接退出`dfs`，并且能够在有环后不进行更深层次的递归，优化程序速度。


# 代码

```java
class Solution {
    private Map<Integer, List<Integer>> graph;
    private boolean[] marked;
    private boolean[] cycle;
    private boolean hasCycle;
    
    public void createGraph(int numCourses, int[][] prerequisites)
    {
        //存储点和他们的邻接边
        graph = new HashMap<>(numCourses);
        //初始化图
        for (int i = 0; i < numCourses; i++) graph.put(i, new LinkedList<>());
        //添加有向边
        for (int i = 0; i < prerequisites.length; i++) graph.get(prerequisites[i][1]).add(prerequisites[i][0]);

        //标记数组
        marked = new boolean[numCourses];
        //负责判断是否有环的临时数组
        cycle = new boolean[numCourses];
    }
    
    /**
     * 拓扑排序相关问题
     * 有向图,判断是否有环
     * 构造图,dfs判断即可
     */
    public boolean canFinish(int numCourses, int[][] prerequisites)
    {
        createGraph(numCourses,prerequisites);
        
        for (int i = 0; i < numCourses; i++)
        {
            //以没标记过的顶点作为某个根节点进行深搜
            if (!marked[i]) dfs(i);
        }
        //无环则可上课
        return !hasCycle;
    }

    private void dfs(int v)
    {
        //顶点标记为已访问
        marked[v] = true;
        cycle[v] = true;
        for (Integer w : graph.get(v))
        {
            if(hasCycle) return;//为了避免有环还在不断寻找
            if (!marked[w])
            {
                dfs(w);
            }
            else if(cycle[w])
            {
                hasCycle = true;
                return;
            }
        }
        cycle[v] = false;
    }
}
```

