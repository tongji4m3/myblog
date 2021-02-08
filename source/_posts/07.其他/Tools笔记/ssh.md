---
title: SSH常用命令与使用
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: '一些常用工具的笔记,主要写了SSH常用命令与使用'
categories: 常用工具
tags:
  - 工具
  - SSH
abbrlink: 50d6952b
date: 2020-06-22 00:00:00
---

### 连接

```java
Tools——Deployment——Configuration 

点击加号  选择SFTP

SSH configuration需要额外配置

配置Mappings ,即本地资源路径和远程路径的映射

Local path是本地资源路径，Deployment path on server 是远程服务器对应的文件路径 
```



### 中文乱码问题

```java
echo $LANG查看字符集

在 /etc/profile配置文件添加export LANG="zh_CN.UTF-8"

. /etc/profile 重新载入
```

 idea SSH连接中文乱码

> File>Settings>Tools>SSH Terminal> Default encoding设为utf-8
>
> 重新启动idea



### 上传文件

>Tools---Deployment---- Remote Host 
>
>一定要选择映射的那个文件夹----右键---Upload here