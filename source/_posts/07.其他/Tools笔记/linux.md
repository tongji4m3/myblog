---
title: linux常用命令与使用
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: '一些常用工具的笔记,主要写了linux常用命令与使用'
categories: 常用工具
tags:
  - 工具
  - linux
abbrlink: 9f1ebbb4
date: 2020-07-30 00:00:00
---

# 基础知识

1. root的家目录为/root,所以~代表了/root。其余的则在/home/用户名
2. /usr/local:系统管理员在本机安装自己下载的软件建议安装的目录





# 常用操作

1. \为转义字符，可以后跟回车，使命令连续到下一行

2. tab tab，命令补全

3. man 命令，查看用法

4. ctrl+C终止命令

5. ctrl+D退出终端

6. > 目录操作
  >
  > cd 
  >
  > pwd 
  >
  > mkdir         -p可以递归创建
  >
  > rmdir          -r可以删除有文件的目录

7. >  文件操作
  >
  > cp 源文件 目标位置  -r可以复制目录
  >
  > rm  -rf  文件/目录   递归删除,且不会出现提示信息
  >
  > mv test test1 可以实现更名操作

8. > 查找文件
  >
  > find /usr -name "jdk*" -type d   查找在/usr下查找目录包含jdk的文件

9. > 解压缩
  >
  > tar -zxv -f filename.tar.gz  -C 解压缩的目录

# vim

1. >三种模式:一般模式,编辑模式,命令行模式
	>
	>一般模式按i进入编辑模式,输入/进入命令行模式.其他两个模式按ESC退出到一般模式

2. > 退出:
	>
	> :wq 保存退出
	>
	> :q! 强制退出不保存

3. > 一般模式
	>
	> Page UP,Page DOWN翻页
	>
	> HOME,END移动到该行首/尾
	>
	> G移动到末尾,数字G移动到某行,1G则可以移动到开头

4. > 查找
	>
	> /word向下继续查找
	>
	>  n为重复前一个查找操作,所以可以配合着向下找.N则向上找

5. > 删除一整行 dd
	>
	> 复制一整行 yy
	>
	> 将复制数据粘贴 p
	>
	> 撤销前一个操作 u

	

# 进程管理

1. ps aux 查看所有进程
2. top 动态查看进程 默认以CPU占用率排序 查看即时活跃的进程，类似Windows的任务管理器
3. 查看端口是否占用: netstat -tunlp |grep 8000
4.  ps -ef | grep -i java
5.  kill -s 9 xxx







