---
title: Java基础--IO
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: 'Java基础知识之IO,待完善,之后再看的时候会继续补充。'
categories: Java基础
tags:
  - Java基础
  - IO
abbrlink: 48185b72
date: 2020-03-02 00:00:00
---

## IO
1. 用完流要调用close()关闭
2. 最终输出前,调用flush(),清空管道
3. 以Stream结尾都是字节流,以Reader/Writer结尾都是字符流

```java
public static void main(String[] args)
{
    FileInputStream fileInputStream = null;
    FileOutputStream fileOutputStream = null;
    try
    {
        fileInputStream = new FileInputStream("src/test.txt");
        fileOutputStream = new FileOutputStream("src/test1.txt");

        byte[] bytes = new byte[1024*1024];//一次读取1024*1024个字节
        int count;//读到的字节数量,读取不到返回-1
        while((count=fileInputStream.read(bytes))!=-1)
        {
            //把读到的byte数组再写出去
            fileOutputStream.write(bytes,0,count);
        }

        fileOutputStream.flush();
    }
    catch (FileNotFoundException e)
    {
        e.printStackTrace();
    }
    catch (IOException e)
    {
        e.printStackTrace();
    }
    finally
    {
        if(fileInputStream!=null)
        {
            try
            {
                fileInputStream.close();
            }
            catch (IOException e)
            {
                e.printStackTrace();
            }
        }
        if(fileOutputStream!=null)
        {
            try
            {
                fileOutputStream.close();
            }
            catch (IOException e)
            {
                e.printStackTrace();
            }
        }
    }
}
```

```java
//自带缓冲
//包装类模式
BufferedReader bufferedReader = new BufferedReader(new FileReader("src/test.txt"));

String line;//不读换行符
while((line=bufferedReader.readLine())!=null)
    System.out.println(line);

//只需要关闭最外层的流
bufferedReader.close();
```

![image-20200808071748335](https://tongji4m3.oss-cn-beijing.aliyuncs.com/image-20200808071748335.png)


```java
//转换流
BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(new FileInputStream("src/test.txt")));
```

## 序列化
1. 要实现标志接口 `Serializable`,会自动生成序列化版本号
2. transient:不参与序列化
3. 通过类名,序列号区分一个类
4. 建议将序列号手动写出来,这样类改动也还能用之前序列化后的



```java
Person person = new Person("zhangsan",23);

ObjectOutputStream objectOutputStream = 
    new ObjectOutputStream(new FileOutputStream("person"));

objectOutputStream.writeObject(person);

objectOutputStream.flush();
objectOutputStream.close();
```
```java
ObjectInputStream objectInputStream = 
    new ObjectInputStream(new FileInputStream("person"));
Object object = objectInputStream.readObject();
System.out.println(object);
objectInputStream.close();
```