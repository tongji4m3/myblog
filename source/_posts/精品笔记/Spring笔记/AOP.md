---
title: Spring AOP学习笔记
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: Spring AOP学习笔记
categories: Spring AOP学习笔记
tags:
  - Spring
  - AOP
  - 动态代理
abbrlink: ca1ec03d
date: 2020-08-08 00:00:00
---



面向切面编程

横切面问题例如:日志,执行时间,权限,事务

AOP编程思想就是把横切面问题(与主业务关联不大的代码)和主业务逻辑进行分离,达到解耦的目的



带着问题去看源码 找出代理对象,返回对象



当放入容器时,对象已经被代理了

# 动态代理

## 基于接口的动态代理

最少实现了一个接口,JDK官方提供

```java
        //要被代理的对象
        final Test test = new TestImpl();
        //args:被代理对象的类加载器,被代理对象的类的接口,用于提供增强代码的InvocationHandler
        //得到代理对象(Object)类型
        Test proxyTest=(Test)Proxy.newProxyInstance(test.getClass().getClassLoader(),test.getClass().getInterfaces() , new InvocationHandler()
        {
            /**
             *执行被代理对象的任何接口方法都会经过该方法
             *
             * @param proxy 代理对象的引用
             * @param method 当前执行的方法
             * @param args  当前执行方法所需要的参数
             * @return 和被代理对象方法有相同的返回值
             * @throws Throwable
             */
            public Object invoke(Object proxy, Method method, Object[] args) throws Throwable
            {
                System.out.println("方法执行前");
                //传入的是被代理对象
                Object result = method.invoke(test, args);
                System.out.println("方法执行后");
                return result;
            }
        });
        int result = proxyTest.add(1, 3);
        System.out.println(result);
```



## CGLIB动态代理

适用没有接口的情况,被代理类不能是最终类

```java
//要被代理的对象
        final Test test = new TestImpl();
        //args 被代理对象的字节码,用于提供增强代码的Callback(使用其子类MethodInterceptor)
        Test cglibTest=(Test)Enhancer.create(test.getClass(), new MethodInterceptor()
        {
            //前三个参数和Proxy的作用一样
            public Object intercept(Object proxy, Method method, Object[] args, MethodProxy methodProxy) throws Throwable
            {
                System.out.println("方法执行前");
                //传入的是被代理对象
                Object result = method.invoke(test, args);
                System.out.println("方法执行后");
                return result;
            }
        });
        int result = cglibTest.add(1, 3);
        System.out.println(result);
```

# 术语

1. 连接点:可以被增强的方法
2. 切入点:实际被增强的方法
3. 通知:实际增强的逻辑部分
4. 切面:把通知应用到切入点的过程

## 通知

1. 前置通知
2. 后置通知 
3. 异常通知 
4. 最终通知 
5. 环绕通知 