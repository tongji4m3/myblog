---
title: LeetCode刷题笔记142
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
  - 链表
  - 快慢指针
abbrlink: 90dcb197
date: 2020-06-04 00:00:00
---

> 题目出自LeetCode
>
> [142. 环形链表 II](https://leetcode-cn.com/problems/linked-list-cycle-ii/)
>
> 
>
> 其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述
给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

说明：不允许修改给定的链表。

 

示例 1：
```
输入：head = [3,2,0,-4], pos = 1
输出：tail connects to node index 1
解释：链表中有一个环，其尾部连接到第二个节点。
```

示例 2：
```
输入：head = [1,2], pos = 0
输出：tail connects to node index 0
解释：链表中有一个环，其尾部连接到第一个节点。
```

示例 3：
```
输入：head = [1], pos = -1
输出：no cycle
解释：链表中没有环。
```


# 思路
先让快慢指针相遇,再让一个指针从头开始,与慢指针同时向后走,他们相遇,则到了入口(可通过画图证明正确性)
# 细节

在判断有没有循环链表的时候就先把没有循环的链表直接返回,避免之后找首节点的逻辑错误

# 代码

```java
public ListNode detectCycle(ListNode head)
{
    ListNode fast = head, slow = head;
    while (true)
    {
        if(fast == null || fast.next == null) return null;
        fast = fast.next.next;
        slow = slow.next;
        if (slow == fast) break;
    }
    //必然有循环
    fast = head;
    while (true)
    {
        if(slow==fast) return fast;
        fast = fast.next;
        slow = slow.next;
    }
}
```


