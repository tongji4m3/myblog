---
title: LeetCode刷题笔记141
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
abbrlink: 9d5e02d
date: 2020-06-03 00:00:00
---

> 题目出自LeetCode
>
> [141. 环形链表](https://leetcode-cn.com/problems/linked-list-cycle/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述
给定一个链表，判断链表中是否有环。

如果链表中有某个节点，可以通过连续跟踪 next 指针再次到达，则链表中存在环。 为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。注意：pos 不作为参数进行传递，仅仅是为了标识链表的实际情况。

如果链表中存在环，则返回 true 。 否则，返回 false 。

```
输入：head = [3,2,0,-4], pos = 1
输出：true
解释：链表中有一个环，其尾部连接到第二个节点。
```

```
输入：head = [1,2], pos = 0
输出：true
解释：链表中有一个环，其尾部连接到第一个节点。
```

```
输入：head = [1], pos = -1
输出：false
解释：链表中没有环。
```

提示：

```
链表中节点的数目范围是 [0, 104]
-105 <= Node.val <= 105
pos 为 -1 或者链表中的一个 有效索引 。
```


# 代码

```java
public boolean hasCycle(ListNode head)
{
    ListNode fast = head, slow = head;
    while(fast!=null && fast.next!=null)
    {
        fast = fast.next.next;
        slow = slow.next;
        if(fast==slow) return true;
    }
    return false;
}
```

