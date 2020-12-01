---
title: Java基础--String
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: 'Java基础知识之String,待完善,之后再看的时候会继续补充。'
categories: Java基础
tags:
  - Java基础
  - String
abbrlink: a0a3a5a1
date: 2020-03-10 00:00:00
---
# String

```
private final char value[];
```

数组长度不可变,而且加了final,所以只能指向那个对象,所以不可变

# println

输出任何数据都转换成字符串再输出

## pringf

```java
System.out.printf("%8.2f",x);
//s为字符串，f为浮点数，d为十进制数
//用8字符的宽度和小数点后两位的精度打印x
//.2如果用在String则表示打印String时输出字符的最大数量
//%-10 则为左对齐
```



## System.out.println(new Object());

```java
public void println(Object x) 
{
    String s = String.valueOf(x);
    synchronized (this) 
    {
        print(s);
        newLine();
    }
}

public static String valueOf(Object obj) 
{
    return (obj == null) ? "null" : obj.toString();
}
```

## System.out.println(1);

```java
public void println(int x) 
{
    synchronized (this) 
    {
        print(x);
        newLine();
    }
}
public void print(int i) 
{
    write(String.valueOf(i));
}
```

