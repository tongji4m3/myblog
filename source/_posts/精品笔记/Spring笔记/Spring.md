---
title: Spring学习笔记
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: Spring学习笔记
categories: Spring学习笔记
tags:
  - Spring
  - 框架
  - Bean
abbrlink: 52ba89f4
date: 2020-08-04 00:00:00
---

# Spring概述

轻量级开源的JavaEE框架

IOC:(Inversion Of Control)控制反转,把创建对象过程交给Spring管理,降低耦合度

AOP:面向切面,不修改源代码进行功能增强

![image-20200818165454094](https://tongji4m3.oss-cn-beijing.aliyuncs.com/image-20200818165454094.png)



## 优点

**1.方便解耦，简化开发**

**2.AOP编程的支持**

**3.声明式事务的支持**

**4.方便程序的测试**

**5.方便集成各种优秀框架**

**6.降低Java EE API的使用难度**

**7.Java 源码是经典学习范例**




# Spring IOC 用法
## Spring各个包
spring-core:包含Spring 框架基本的核心工具类
spring-beans:IOC容器必备jar包,包含(IoC/DI）操作相关的所有类
spring-expression:表达式解析,支持在运行时动态的解析表达式给对象赋值
spring-aop:使用Spring 的AOP 特性时所需的类和源码级元数据支持
spring-context:可以找到使用Spring ApplicationContext特性时所需的全部类,会自动将 spring-core、spring-beans、spring-aop、spring-expression
## Bean作用范围

通过@Scope指定

singleton:单例(默认)

prototype:多例

## 生命周期

1. 通过无参构造器创建bean实例
2. 调用set方法为bean的属性赋值
3. 把bean实例传递给bean后置处理器
4. 调用bean的初始化方法
5. 把bean实例传递给bean后置处理器
6. 获取到bean对象
7. 容器关闭,调用bean销毁方法

## 核心容器两个接口

ApplicationContext:在创建核心容器时,创建对象采取立即加载的形式,只要一读取配置文件就立即创建配置文件中的对象

BeanFactory:采用延迟加载的方式,什么时候根据id获取对象才真正创建容器

## 常用注解
1. @Component
2. @Service
3. @Controller
4. @Repository 用于数据访问层(Dao层),Mapper中
5. @Autowired
6. @Value 注入普通类型属性
7. @Configuration 声明为配置类
8. @ComponentScan("com.tongji") 配置扫描包






## 创建 Bean 容器

## 初始化 Bean





控制反转,核心在于反射,通过反射创建对象,操作对象

bean的实例化过程,创建的生命周期.有很多的Processor,提高扩展性

监听器

框架,一定要提高扩展性



在对象创建之前添加某些功能

在容器初始化之前添加某些功能

在不同的阶段发出不同的事件,完成某些功能

抽象出一堆接口来帮助扩展

面向接口编程



从new,到工厂模式,到容器



创建对象时,默认调用无参数构造方法完成对象创建