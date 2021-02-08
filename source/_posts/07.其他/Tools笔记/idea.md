---
title: idea常用命令与使用
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: '一些常用工具的笔记,主要写了idea常用命令与使用'
categories: 常用工具
tags:
  - 工具
  - idea
abbrlink: e0571985
date: 2020-04-14 00:00:00
---

# 设置

---

1. File Export Settings先导出一份自己熟悉使用的设置，导出为 settings.jar.新电脑就直接file import Settings

2. 下载ultimate版本的,注册可以用去官网学生认证

3. 全屏，view，appearance，full screen；如果顶部菜单栏不见了，改ui.inf.xml的<option name="SHOW_MAIN_MENU" value="false" />这个选项为false，将其修改为true

4. 大小写不敏感：setting->Editor->General->Code Completion取消Match case

5. 花括号File->Setting->Editor->Code Style->Java->Wrapping and Braces

6. > 自定义模板
   >
   > File –> Setting中, 搜索live…要设置下面的change，选java
   >
   > fori不用配置
   >
   > 集合.for增强for循环快捷键  
   >
   > sys:System.out.print($END$);

7. ctrl+F8设置断点,改成ctrl+shift+B,记得去除之前的一个

8. 格式化 ctrl+shift+F,在右边搜索栏输入：reformat code 

9. Args传入参数：Run下的Edit Configurations，配置Configuration分页中的Program arguments选项

10. Ctrl+鼠标滑轮控制字体大小，在File -> Setting -> Editor -> General下进行设置。选中Change font size (Zoom) with Ctrl+Mouse wheel 

11. 设置idea背景,File | Settings | Appearance & Behavior | Appearance|background Image

   

---

# 快捷键(常用)

1. Alt+enter内容辅助，可以这样比较方便的新建一个类,或者是修改建议

1. Ctrl +Y 删除代码
2. 代码的上下移动，ctrl+shift+上下箭头
3. shift+F6 重命名
4. 格式化 ctrl+shift+F
5. Ctrl+D 复制当前行到下一行
6. ctrl+/；ctrl+shift+/  注释
7. Alt+ins，快速生成get，set等等
8. Alt+1打开层次体系
9. 行末加分号，ctrl+shift+enter
10. 用F2移动到有错误的代码
11. Ctrl+alt+ins快速新建类
12. ctrl+shift+加减,代码折叠 
13. 选中类名 Ctrl+鼠标点击  查看源码
14. shift+enter 快速下一行
15. Ctrl+删除，删除这个单词
16. .Ctrl+F搜索
17. ctrl+左右，快速跳过一个单词;Shift+上下,选中某行；



---

# 快捷键(常忘记的)

1. 运行：Alt+Shift+F10运行程序，Shift+F9启动调试，Ctrl+F2停止。Ctrl+F8 设置断点 。F7/F8/F9分别对应Step into，Step over，Continue，shift+F8退出方法
2. 抽取方法快捷键:ctrl+alt+m
3. Ctrl+H打开类继承体系，ctrl+F12查看类所有方法
4. Ctrl+Alt+V则是抽取变量
5. Ctrl+W快速选中一行
6. Ctrl+Tab切换类
7. Shift+shift快速搜索，可以查找类
8. Ctrl+alt+s 打开设置
9. ctrl alt+t 用try catch等包裹代码
10. shift+end或者home,快速选择一行
11. ctrl+p方法参数提示



# 整合github

在IDEA中设置GitHub，File-->Setting->Version Control-->GibHub

创建本地仓库，VCS-->Import into Version Control-->Create Git Repository

VCS-->Import into Version Control-->Share Project on GitHub

# UML

1. 右键一个类--Diagram--show Diagrams
2. 对一个类,右键,可用`show Parents`,`show implementations`
3. 也可以新添加类,对一个类按空格

