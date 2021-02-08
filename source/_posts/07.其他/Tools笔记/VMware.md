---
title: VMware常用命令与使用
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: '一些常用工具的笔记,主要写了VMware常用命令与使用'
categories: 常用工具
tags:
  - 工具
  - VMware
abbrlink: d398cc0d
date: 2020-05-25 00:00:00
---


# 配置Ubuntu

## [教程](https://blog.csdn.net/stpeace/article/details/78598333)
## 设置root密码
`ctrl+alt+F3`切换命令行,设置root: `sudo passwd root`,设置密码,确认密码

## ssh连接
### [教程](https://blog.csdn.net/weixin_42739326/article/details/82260588?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-2.channel_param)
### ssh连接允许root登录
修改`/etc/ssh/sshd_config`下的`PermitRootLogin yes`
		重新启动服务`/etc/init.d/ssh restart`
### 用idea管理ssh连接
[教程](https://blog.csdn.net/weixin_42249196/article/details/107464658)
或者可以用idea连接进行命令行操作,用Xftp进行文件上传操作

## 快照
为便于出错后的恢复,最好在具体操作之前做好快照
`对虚拟机项目右键-快照-拍摄快照`

## 配置镜像源

[教程](https://blog.csdn.net/u013541411/article/details/81410964)


# 配置centos7
## [教程](https://blog.csdn.net/qq_39135287/article/details/83993574?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-4.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-4.channel_param)

yum不可用,更换源:[教程](https://blog.csdn.net/qq_41684957/article/details/83345154?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.channel_param)

## [ssh连接](https://blog.csdn.net/mengzuchao/article/details/80261836)
