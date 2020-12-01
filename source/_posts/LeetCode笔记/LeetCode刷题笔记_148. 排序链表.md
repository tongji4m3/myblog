---
title: LeetCode刷题笔记148
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
  - 链表
  - 排序
abbrlink: '70095889'
date: 2020-06-08 00:00:00
---

> 题目出自LeetCode
>
> 148. 排序链表
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序。
```
示例 1:

输入: 4->2->1->3
输出: 1->2->3->4
```
```
示例 2:

输入: -1->5->3->4->0
输出: -1->0->3->4->5
```

# 思路

归并法排序,用循环合并两个有序数组

# 细节

1. fast可以先等于head.next,避免将两条链表断开的麻烦操作
2. 对一个链表继续递归进行`sortList`时,注意接收传回的引用

# 代码

```java
public ListNode sortList(ListNode head)
{
    if (head == null || head.next == null) return head;

    //将链表大致平分成head,slow两条
    //look 先将fast向后移动一位,这样切分单数数组就是前面少一个,后面多一个.切分双数正好相等
    //而且这样可以减少处理的麻烦
    ListNode slow = head, fast = head.next;
    while (fast != null && fast.next != null)
    {
        fast = fast.next.next;
        slow = slow.next;
    }
    ListNode second = slow.next;
    slow.next = null;//为了断开中点前一个节点与中点之间的连接


    head = sortList(head);//look,要接收改变后的链表的引用
    second = sortList(second);

    //对两条有序链表进行合并操作
    ListNode pre = new ListNode(-1);
    ListNode temp = pre;

    while (head != null && second != null)
    {
        int value = 0;
        if (head.val < second.val)
        {
            value = head.val;
            head = head.next;
        }
        else
        {
            value = second.val;
            second = second.next;
        }
        temp.next = new ListNode(value);
        temp = temp.next;
    }
    temp.next = (head == null ? second : head);

    return pre.next;
}
```



