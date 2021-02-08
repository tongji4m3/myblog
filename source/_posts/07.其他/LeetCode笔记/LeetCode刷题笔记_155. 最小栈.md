---
title: LeetCode刷题笔记155
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
  - 栈
  - 算法
abbrlink: 17a31575
date: 2020-06-13 00:00:00
---

> 题目出自LeetCode
>
> [155. 最小栈](https://leetcode-cn.com/problems/min-stack/)
>
> 
>
> 其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述
设计一个支持 push ，pop ，top 操作，并能在常数时间内检索到最小元素的栈。
```
push(x) —— 将元素 x 推入栈中。
pop() —— 删除栈顶的元素。
top() —— 获取栈顶元素。
getMin() —— 检索栈中的最小元素。
```

示例:
```
输入：
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

输出：
[null,null,null,null,-3,null,0,-2]

解释：
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.

```

提示：

pop、top 和 getMin 操作总是在 非空栈 上调用。



# 思路

多用一个栈保存最小值

# 细节

栈与存储最小元素的辅助栈最小元素要一一对应,不能因为重复就不存了.

# 代码

```java
public class MinStack
{
    Deque<Integer> stack;
    Deque<Integer> minStack;


    public MinStack()
    {
        stack = new LinkedList<>();
        minStack = new LinkedList<>();
    }

    public void push(int x)
    {
        stack.push(x);
        //小于等于都存,一一对应,好删除
        if (minStack.isEmpty() || x <= minStack.peek()) minStack.push(x);
    }

    public void pop()
    {
        if(stack.pop().equals(minStack.peek())) minStack.pop();
    }

    public int top()
    {
        if (stack.isEmpty()) throw new RuntimeException();
        return stack.peek();
    }

    public int getMin()
    {
        if (minStack.isEmpty()) throw new RuntimeException();
        return minStack.peek();
    }
}
```



