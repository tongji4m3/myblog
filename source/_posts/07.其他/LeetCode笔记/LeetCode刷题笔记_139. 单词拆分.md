---
title: LeetCode刷题笔记139
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
  - 动态规划
abbrlink: 484ffed8
date: 2020-06-01 00:00:00
---

> 题目出自LeetCode
>
>  139.单词拆分
>
>  其他题解或源码可以访问： [tongji4m3](https://github.com/tongji4m3/LeetCode)



# 描述

给定一个非空字符串 s 和一个包含非空单词的列表 wordDict，判定 s 是否可以被空格拆分为一个或多个在字典中出现的单词。

说明：

拆分时可以重复使用字典中的单词。
		你可以假设字典中没有重复的单词。
示例 1：

```
输入: s = "leetcode", wordDict = ["leet", "code"]
输出: true
解释: 返回 true 因为 "leetcode" 可以被拆分成 "leet code"。
```
示例 2：
```
输入: s = "applepenapple", wordDict = ["apple", "pen"]
输出: true
解释: 返回 true 因为 "applepenapple" 可以被拆分成 "apple pen apple"。
     注意你可以重复使用字典中的单词。
```
示例 3：
```
输入: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
输出: false
```

# 思路

```
动态规划
dp[i]代表s.substring(0,i)能否被表示
dp[0]=true
return dp[s.length()]
dp[i]=
	for j in [0,i):
		只要包含了一个(前一部分存在,剩下的那个单词在wordDict中)
		
```





# 代码

```
public boolean wordBreak(String s, List<String> wordDict)
{
    if(s==null || s.length()==0) return false;
    boolean[] dp = new boolean[s.length() + 1];
    dp[0] = true;
    for (int i = 0; i < dp.length; i++)
    {
        for (int j = 0; j < i; j++)
        {
            if (dp[j] && wordDict.contains(s.substring(j, i)))
            {
                dp[i] = true;
                break;//look 找到一个即可,不用继续找了
            }
        }
    }
    return dp[s.length()];
}
```


