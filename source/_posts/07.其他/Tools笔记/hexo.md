---
title: hexo常用命令与使用
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: '一些常用工具的笔记,主要写了hexo常用命令与使用'
categories: 常用工具
tags:
  - 工具
  - hexo
abbrlink: 95af1e01
date: 2020-07-14 00:00:00
---

## 一.安装hexo

搭建可以参考视频:[CodeSheep搭建博客教程](https://www.bilibili.com/video/BV1Yb411a7ty?from=search&seid=17889294783077443284),如果出现问题可以看弹幕解决

**连接Github时注意**

>git config --global user.name "Github名字"
>
>git config --global user.email "Github绑定的邮箱"

**中文乱码**

> echo $LANG查看字符集
>
> 在 /etc/profile配置文件添加export LANG="zh_CN.UTF-8"
>
>  . /etc/profile 重新载入

**idea ssh连接中文乱码**

> File>Settings>Tools>SSH Terminal> Default encoding设为utf-8

## 二.hexo主题与美化

主题可以用[next主题](https://github.com/iissnan/hexo-theme-next)上的，在next主题上进行美化:[next美化教程](https://blog.csdn.net/nightmare_dimple/article/details/86661502)

另一个教程:[hexo美化设置](https://blog.csdn.net/qincidong/article/details/82415256)

目前正在使用的,**强烈推荐**:[Matery主题](https://github.com/blinkfox/hexo-theme-matery)

> hexo相关的设置在blog/_config.yml文件修改_
>
> 主题相关的设置在themes/next/_config.yml文件修改

## 三.hexo相关命令

> hexo d 部署到Github上
>
> hexo clean清空缓存



