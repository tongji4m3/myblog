---
title: LeetCode刷题笔记146
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
  - Map
  - LRU
abbrlink: 97b1758e
date: 2020-06-06 00:00:00
---

> 题目出自LeetCode
>
> 146. LRU缓存机制
>
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。它应该支持以下操作： 获取数据 get 和 写入数据 put 。

获取数据 get(key) - 如果关键字 (key) 存在于缓存中，则获取关键字的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组「关键字/值」。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

 

进阶:

你是否可以在 O(1) 时间复杂度内完成这两种操作？

 

示例:

```

LRUCache cache = new LRUCache( 2 /* 缓存容量 */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // 返回  1
cache.put(3, 3);    // 该操作会使得关键字 2 作废
cache.get(2);       // 返回 -1 (未找到)
cache.put(4, 4);    // 该操作会使得关键字 1 作废
cache.get(1);       // 返回 -1 (未找到)
cache.get(3);       // 返回  3
cache.get(4);       // 返回  4
```

# 思路

1. 可以使用`LinkedHashMap`,已经封装好了方法,只需要重写`removeEldestEntry`方法即可
2. 自己实现逻辑,则使用双向链表与哈希表结合,其实就是上述1方法的具体实现方式

# 细节

# 代码

```java
public class LRUCache
{
    private Map<Integer, Node> map;//存储的是key,Node
    DoubleList cache;//用于保证删除是O(1)
    private int capacity;

    private class Node
    {
        int key;
        int value;
        Node next;
        Node pre;

        Node(int key, int value)
        {
            this.key = key;
            this.value = value;
        }
    }

    private class DoubleList
    {
        Node first;//头尾虚节点
        Node last;
        int size;

        DoubleList()
        {
            first = new Node(0, 0);
            last = new Node(0, 0);
            first.next = last;
            last.pre = first;
            size = 0;
        }

        void addFirst(Node node)
        {
            node.pre=first;
            node.next=first.next;
            first.next.pre=node;
            first.next=node;
            ++size;
        }

        Node remove(Node node)
        {

            node.pre.next = node.next;
            node.next.pre = node.pre;

            node.pre = null;
            node.next = null;

            --size;

            return node;
        }

        Node removeLast()
        {
            if(size==0) return null;
            return remove(last.pre);
        }


    }

    public LRUCache(int capacity)
    {
        this.map = new HashMap<>();
        this.cache = new DoubleList();
        this.capacity = capacity;
    }

    public int get(int key)
    {
        if (!map.containsKey(key)) return -1;
        int value = map.get(key).value;
        put(key, value);
        return value;
    }

    public void put(int key, int value)
    {
        Node node = new Node(key, value);
        if (map.containsKey(key))
        {
            cache.remove(map.get(key));
            cache.addFirst(node);
        }
        else
        {
            if (capacity == cache.size)
            {
                Node last = cache.removeLast();
                map.remove(last.key);//这是为什么Node要存key,val,不能只存val
            }
            cache.addFirst(node);
        }
        map.put(key, node);
    }
}
```

```java
/**
调用库的实现方法

LinkedHashMap<Integer, Integer>
它是一个将所有Entry节点链入一个双向链表的HashMap
此外，LinkedHashMap可以很好的支持LRU算法
它额外维护了一个双向链表用于保持迭代顺序,该迭代顺序可以是插入顺序，也可以是访问顺序。
 * @author 12549
 */
public class LRUCache extends LinkedHashMap<Integer, Integer>
{
    private Integer capacity;
    /*
    当accessOrder标志位为true时，表示双向链表中的元素按照访问的先后顺序排列
    当标志位accessOrder的值为false时，表示双向链表中的元素按照Entry插入LinkedHashMap到中的先后顺序排序
    当我们要用LinkedHashMap实现LRU算法时，就需要调用该构造方法并将accessOrder置为true。
    当accessOrder为true时，get方法和put方法都会调用recordAccess方法使得最近使用的Entry移到双向链表的末尾
     */

    public LRUCache(int capacity)
    {
        super(capacity,0.75F, true);
        this.capacity = capacity;
    }

    public int get(int key)
    {
        return super.getOrDefault(key, -1);
    }

    public void put(int key, int value)
    {
        super.put(key, value);
    }

    /*
    该方法是用来被重写的，一般地，如果用LinkedHashMap实现LRU算法，就要重写该方法。
    比如可以将该方法覆写为如果设定的内存已满，则返回true，
    这样当再次向LinkedHashMap中putEntry时，
    在调用的addEntry方法中便会将近期最少使用的节点删除掉（header后的那个节点）。
     */

    @Override
    protected boolean removeEldestEntry(Map.Entry<Integer, Integer> eldest)
    {
        return size()>capacity;
    }
}
```