---
title: LeetCode刷题笔记76
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
  - 字符串
  - 滑动窗口
abbrlink: d492b0b1
date: 2020-05-07 00:00:00
---

> 题目出自LeetCode
>
> [76. 最小覆盖子串](https://leetcode-cn.com/problems/minimum-window-substring/)
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

给你一个字符串 S、一个字符串 T 。请你设计一种算法，可以在 O(n) 的时间复杂度内，从字符串 S 里面找出：包含 T 所有字符的最小子串。

 

示例：

```
输入：S = "ADOBECODEBANC", T = "ABC"
输出："BANC"
```



提示：

```
如果 S 中不存这样的子串，则返回空字符串 ""。
如果 S 中存在这样的子串，我们保证它是唯一的答案。
```



# 思路

滑动窗口的方法:先扩大hi,使之包含T,然后增加lo,使之最小直到不满足要求。继续循环扩大hi

```
//初步思路
int lo=0,hi=0;//左右指针,指向最小覆盖子串的首尾
int result=0;
while(hi<N) 
{	
	while([lo,hi]区间包含T)
	{
		result=max(result,hi-lo+1);
		++lo;//增加lo
	}
	++hi;//扩大hi
}

```

关键在于如何判断：[lo,hi]区间包含T

可以让map存储T中字符与出现次数,循环中如果出现了T中字符，则加入window中

用一个值判断map与windows中字符的匹配情况（如果一个字符出现的次数相同则匹配）

```
int lo=0,hi=0;//左右指针,指向最小覆盖子串的首尾
int match=0;//匹配情况

for ch in T:
	map.put(ch,map.get(ch)+1)

while(hi<N) 
{
	char ch=T[hi]
	if(map.contains(ch))
	{
		window.put(ch,window.get(ch)+1);
		if(map.get(ch)==window.get(ch)) ++match; //windows中该字符太多不会匹配多次
	}
	//说明至少包含了T所有字符
	while(match==map.size())
	{
		result=max(result,hi-lo+1);
		if(map.contains(T[lo])) //说明滑动了一个T中字符
		{
			window.put(T[lo],window.get(T[lo])-1);//look ch代表的是T[hi]
			if(map.get(T[lo])>window.get(T[lo])) --match;
		}
		++lo;//增加lo
	}
	++hi;//扩大hi
}
```





# 代码

```java
public String minWindow(String s, String t)
{
    int lo=0,hi=0;//左右指针,指向最小覆盖子串的首尾
    int start=0,length=Integer.MAX_VALUE;//look 记录结果 求最小,length应该为最大
    int match = 0;//匹配情况

    Map<Character, Integer> map = new HashMap<>();
    Map<Character, Integer> window = new HashMap<>();//代表滑动窗口
    for (char ch : t.toCharArray())
    {
        map.put(ch, map.getOrDefault(ch, 0) + 1);
    }

    while(hi<s.length())
    {
        char chHi = s.charAt(hi);//look 命名为ch可能导致下面误导用ch表示S[lo]
        if(map.containsKey(chHi)) //如果出现了T中字符,则放入
        {
            window.put(chHi, window.getOrDefault(chHi, 0) + 1);
            if(map.get(chHi).equals(window.get(chHi))) ++match; //windows中该字符太多不会匹配多次
        }
        while(match==map.size())
        {
            if(length>hi-lo+1)
            {
                length = hi - lo + 1;
                start = lo;
            }
            char chLo = s.charAt(lo);
            if(map.containsKey(chLo)) //说明滑动了一个T中字符
            {
                window.put(chLo,window.get(chLo)-1);
                if(map.get(chLo)>window.get(chLo)) --match;
            }
            ++lo;//增加lo
        }

        ++hi;//扩大hi
    }
    //如果不包含这样的子串,那length没变
    if(length==Integer.MAX_VALUE) return "";
    return s.substring(start,start+length);
}
```





