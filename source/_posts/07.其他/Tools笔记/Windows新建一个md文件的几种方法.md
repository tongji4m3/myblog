---
title: 快速新建md文件
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: '一些常用工具的笔记,介绍在windows下如何快速新建md文件'
categories: 常用工具
tags:
  - 工具
  - markdown
abbrlink: b379f77c
date: 2020-08-02 00:00:00
---

﻿# 快捷键新建文档

1. win+r,输入regedit点击运行打开注册表
2. ctrl+F搜索 文本文档
3. 双击此键值，在"文本文档"后加上" (&T)"(不要忘记前面有一个空格)
4. 此时可以用右键+w+t新建文档
5. 再修改文件名和后缀为md文件
# 右键新建md文件
1. 新建文本文件
```
Windows Registry Editor Version 5.00

[HKEY_CLASSES_ROOT\.md]
@="Typora.md"
"Content Type"="text/markdown"
"PerceivedType"="text"

[HKEY_CLASSES_ROOT\.md\ShellNew]
"NullFile"=""
```
2. 修改后缀为reg,双击运行即可

# win+R输入typora运行
