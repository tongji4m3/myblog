---
title: 项目------Web项目-简单的购物网站
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: Web项目-简单的购物网站文档。一个简单的前后端项目，其中前端只用了HTML，Css，JS
categories: 项目文档
tags:
  - HTML
  - JavaScript
  - Springboot
abbrlink: a8f59b26
date: 2020-05-12 00:00:00
---
# 项目简介

本项目是基于BS架构的简单购物网站。主要实现了用户注册登录，商品展示，添加购物车，结算下单，查询历史订单信息五个功能。前后端分为两个项目，都采用了IDEA进行开发。其中前端使用了HTML，CSS，JavaScript技术，并且使用原生ajax向后端发起请求。后端则使用maven管理依赖，使用springboot框架，并且整合了mybatis框架以连接MySQL数据库。并且该项目前后端分离，且严格分离html，css和js。其中，整个项目部署在了云服务器上，访问地址为：

<http://47.103.203.188:8080/project/html/index.html>

源码可在Github上查看:[tongji4m3](https://github.com/tongji4m3/webProject)

# 项目技术架构介绍

## 前端

>   前端项目一共有4个文件夹，分别存储了`html`，`css`，`js`，`img`文件。其中每一个html文件都会引用css，js文件夹中与之对应的文件，并且在主页以及商品详情中引用img文件夹里的相应图片。

>   每个商品的商品详情则是放在了html/productDetails中。图片则根据商品名称放在不同的文件夹下。而ajax请求的路径，则统一放置在了js/api.js文件中。

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/615544abc332617d714709043dbca86c.png)

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/04fdb77cca62acf21e33e753bc975cdc.png)

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/083899cb9561ac40e8dafeac0b44459e.png)

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/e7508c123b5b86102d8d41dc5d5cc9c7.png)

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/fa09cc6d1dbc52e50f4a16820a79e526.png)

## 数据库

>   共分为四个表，user表存储用户信息，product表存储商品信息，shoppingCart存储购物车信息并且关联了user表和product表，myOrder存储订单信息并且关联了user表和product表。

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/2e26a50a7b8e4736fb2340349809f374.png)

## 后端

>   后端使用三层架构的模式，controller包为界面层，负责从前端获取json数据，并且调用业务逻辑层获取相关的数据封装成json格式并且返回给前端。而service包下为业务逻辑层，主要负责进行一些业务处理，并且调用数据访问层得到数据并返回给界面层。mapper包下负责查询数据库，获取相关信息，并且将一些信息封装成实体类并且返回给业务逻辑层。domain包下则是一个个实体类。

>   controller包下主要有三个类，分别负责对用户登录注册等功能的处理的UserController类，对购物车和订单操作的处理的OperatorController类，以及返回验证码的CheckCodeController类。

>   service包下基本就是对应于controller包下三个类的对应接口和实行类。mapper包下就是对应于controller包下三个类的接口，他们的具体逻辑实现通过xml配置文件实现。

>   domain包下分别有用户，商品，购物车，订单的实体类，并且还有一个封装了要返回信息的ResultInformation类。

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/e6fa4af191f391f3aa29ad41014470d3.png)

#  项目功能介绍

## 首页

>   首页主要实现了一个首页导航栏以及商品简略信息的查看功能，导航栏能跳转到登录，注册，购物车，订单页面中。并且实现了对登录者用户名的存储，展示以及注销功能。商品简略信息则有一些动态效果，并且点击能跳转到相应的商品详情页面。

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/803e7752c2cb01a3b406c7cc2284f798.png)

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/2ae59d5f365c24d7d4ef356712e4c3e0.png)

## 用户注册登录

>   登录于注册功能都有对表单的校验功能，并且注册功能还有验证码功能，点击可以动态刷新，但是由于跨域session存储不了的问题，后端没有去校验验证码。

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/f6cf9544375e71bab20397f08978c4bd.png)

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/f88237bd17dc0dbee7b23d8c7e8b89b7.png)

## 商品详情页面

>   每个商品的商品详情中，有一个导航栏，有一个定时切换商品不同图片的轮播图，以及商品详情的文字描述，以及加入购物车和立即购买按钮，两个按钮都会判断是否登录而采取不同动作。

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/0dcbe38556203a7b32055ca2e384ecc9.png)

## 添加购物车

>   在商品详情点击添加购物车后，如果未登录，将跳转到登录界面，否则将之加入购物车，并且前往购物车界面，购物车页面会展示已经加入购物车的商品，并且可以选择购买或者删除该商品。

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/40a0aab6c095373eaddc834c12ca7036.png)

## 结算下单

当在商品详情选择立即购买，或者在购物车点击购买时，将跳转到购买界面，显示要购买的商品，以及购买人的信息。点击购买，则模拟购买成功，并且跳转到历史订单界面。

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/debe58129dc0bfdc1597629e0945ce7d.png)

## 历史订单查询

登录状态才能进入历史订单页面，进入后将展示购买过的商品，并且可以删除订单。

![](https://tongji4m3.oss-cn-beijing.aliyuncs.com/57c5639f4db15bda5e7cb79bcc7db8bf.png)
