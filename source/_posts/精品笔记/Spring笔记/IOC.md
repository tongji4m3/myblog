---
title: Spring IOC学习笔记
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: Spring IOC学习笔记
categories: Spring IOC学习笔记
tags:
  - Spring
  - IOC
  - BeanFactory
abbrlink: c5ac6ae
date: 2020-08-06 00:00:00
---

# 一些概念

## BeanFactory

BeanFactory就是Bean工厂，所有的Bean都由BeanFactory统一创建和管理。提供了框架和基本功能

## AbstractBeanFactory

```
public <T> T getBean(String name, Class<T> requiredType) throws BeansException
{
    return doGetBean(name, requiredType, null, false);
}
```

根据名字和类型获取Bean对象，如果BeanFactory中存在Bean，则从缓存中取Bean，否则创建并返回该Bean，并且将该Bean添加到缓存中(这里指Singleton类型的Bean)。

## ApplicationContext

在BeanFactory 简单IOC容器的基础上添加了许多对高级容器的支持。ApplicationContext容器通过读取配置元数据来获取要实例化，配置和组装哪些对象的指令。

## AbstractApplicationContext
ApplicationContext接口的抽象实现，没有强制规定配置的存储类型，仅仅实现了通用的上下文功能。这个实现用到了模板方法设计模式，需要具体的子类来实现其抽象方法。自动通过registerBeanPostProcessors()方法注册BeanFactoryPostProcessor, BeanPostProcessor和ApplicationListener的实例用来探测bean factory里的特殊bean

## BeanDefinition

BeanDefinition 是一个接口，它是用来存储Bean定义的一些信息的，比如ClassName，Scope，lifecycle,init-methon等等，BeanDefinition 抽象了对 Bean的定义。

## DefaultListableBeanFactory

也实现了BeanFactory和BeanDefinitionRegistry接口，拥有Bean对象管理和BeanDefinition注册功能。AnnotationConfigApplicationContext是委托DefaultListableBeanFactory来实现对象管理和BeanDefinition注册的。这里使用的是代理模式。

## AnnotationConfigRegistry
注解配置注册表。用于注解配置应用上下文的通用接口，拥有一个注册配置类和扫描配置类的方法
## BeanDefinitionRegistry
用于持有像RootBeanDefinition和 ChildBeanDefinition实例的bean definitions的注册表接口。DefaultListableBeanFactory实现了这个接口，因此可以通过相应的方法向beanFactory里面注册bean。GenericApplicationContext内置一个DefaultListableBeanFactory实例，它对这个接口的实现实际上是通过调用这个实例的相应方法实现的。



## GenericApplicationContext
通用应用上下文，内部持有一个DefaultListableBeanFactory实例，这个类实现了BeanDefinitionRegistry接口，可以在它身上使用任意的bean definition读取器。

## AnnotationConfigApplicationContext

这个类是基于注解的容器类，它实现了BeanFactory和BeanDefinitionRegistry两个接口，拥有Bean对象的管理和BeanDefinition注册功能。同时这个类拥有一个DefaultListableBeanFactory的对象。



# AnnotationConfigApplicationContext继承体系

![image-20200821093635307](https://tongji4m3.oss-cn-beijing.aliyuncs.com/image-20200821093635307.png)


# AnnotationConfigApplicationContext三个构造方法
```java
//最常用的构造函数，通过将涉及到的配置类传递给该构造函数，
//以实现将相应配置类中的Bean自动注册到容器中
public AnnotationConfigApplicationContext(Class<?>... componentClasses) 
{
//初始化ClassPathBeanDefinitionScanner和AnnotatedBeanDefinitionReader
    this();
    this.register(componentClasses);
    this.refresh();
}
```

```java
//默认构造函数，初始化一个空容器，容器不包含任何 Bean 信息
//需要在稍后通过调用其register()
//方法注册配置类，并调用refresh()方法刷新容器，
//触发容器对注解Bean的载入、解析和注册过程
public AnnotationConfigApplicationContext() 
{

    //BeanDefinition解析器,用来解析带注解的bean
    this.reader = new AnnotatedBeanDefinitionReader(this);
    //bean的扫描器,用来扫描类
    this.scanner = new ClassPathBeanDefinitionScanner(this);
}
```

```java
public AnnotationConfigApplicationContext(String... basePackages) 
{
    this();
    this.scan(basePackages);//扫描包、注册bean
    this.refresh();
}
```



# AnnotationConfigApplicationContext() 方法

## AnnotatedBeanDefinitionReader()

```
this.reader = new AnnotatedBeanDefinitionReader(this);
```

```
public AnnotatedBeanDefinitionReader(BeanDefinitionRegistry registry) 
{
    this(registry, getOrCreateEnvironment(registry));
}
```

## ClassPathBeanDefinitionScanner()

```
public ClassPathBeanDefinitionScanner(BeanDefinitionRegistry registry) 
{
    this(registry, true);
}
```

```
public ClassPathBeanDefinitionScanner(BeanDefinitionRegistry registry, 
boolean useDefaultFilters, Environment environment, 
@Nullable ResourceLoader resourceLoader) 
{
    this.beanDefinitionDefaults = new BeanDefinitionDefaults();
    this.beanNameGenerator = AnnotationBeanNameGenerator.INSTANCE;
    this.scopeMetadataResolver = new AnnotationScopeMetadataResolver();
    this.includeAnnotationConfig = true;
    Assert.notNull(registry, "BeanDefinitionRegistry must not be null");
    
    this.registry = registry;//为容器设置加载Bean定义的注册器
    
    if (useDefaultFilters) 
    {
        this.registerDefaultFilters();//是否使用默认过滤规则
    }

    this.setEnvironment(environment);//设置环境
    this.setResourceLoader(resourceLoader);//为容器设置资源加载器
}
```



# refresh()方法

```java
public void refresh() throws BeansException, IllegalStateException
{
    synchronized (this.startupShutdownMonitor)//加锁
    {
        // 准备工作，记录下容器的启动时间、标记“已启动”状态等等
        this.prepareRefresh();
        
        //创建 Bean 容器，初始化 BeanFactory容器,注册BeanDefinition,加载并注册 Bean
        //得到配置文件的信息,并且放到BeanFactory中,Bean还没初始化
        //只是一个(beanName, beanDefinition) 的 map
        ConfigurableListableBeanFactory beanFactory = this.obtainFreshBeanFactory();
        
        
        // 设置 BeanFactory 的类加载器,添加几个 BeanPostProcessor
        this.prepareBeanFactory(beanFactory);

        try
        {
            //BeanFactoryPostProcessor相关 提供给子类的扩展点
            //此时Bean都加载完,但是还没有初始化
            //可以在这步的时候添加一些特殊的 BeanFactoryPostProcessor 的实现类
            this.postProcessBeanFactory(beanFactory);
            
            // 调用 BeanFactoryPostProcessor 
            //各个实现类的 postProcessBeanFactory(factory) 方法
            this.invokeBeanFactoryPostProcessors(beanFactory);
            
            // 注册 BeanPostProcessor 的实现类
         	// 此接口两个方法: 
         	//postProcessBeforeInitialization 和 postProcessAfterInitialization
         	// 两个方法分别在 Bean 初始化之前和初始化之后得到执行。到这里 Bean 还没初始化
            this.registerBeanPostProcessors(beanFactory);
            
            // 初始化当前 ApplicationContext 的 MessageSource，国际化
            this.initMessageSource();
            
            // 初始化当前 ApplicationContext 的事件广播器
            this.initApplicationEventMulticaster();
            
            // 典型的模板方法(钩子方法)，
         	// 具体的子类可以在这里初始化一些特殊的 Bean（在初始化 singleton beans 之前）
            this.onRefresh();
            
             // 注册事件监听器，监听器需要实现 ApplicationListener 接口
            this.registerListeners();
            
            // 初始化所有的 singleton beans
         	//（lazy-init 的除外）
            this.finishBeanFactoryInitialization(beanFactory);
            
            // 广播事件，ApplicationContext 初始化完成
            this.finishRefresh();
        }
        catch (BeansException var9)
        {
            if (this.logger.isWarnEnabled())
            {
                this.logger.warn("Exception encountered during context initialization - cancelling refresh attempt: " + var9);
            }

            // 销毁已经初始化的 singleton 的 Beans，以免有些 bean 会一直占用资源
            this.destroyBeans();
            
            // 设置 'active' 状态
            this.cancelRefresh(var9);
            throw var9;
        }
        finally
        {
            //清除缓存
            this.resetCommonCaches();
        }

    }
}
```



# obtainFreshBeanFactory

```java
protected ConfigurableListableBeanFactory obtainFreshBeanFactory()
{
	//// 关闭旧的 BeanFactory,创建新的 BeanFactory，加载 Bean 定义、注册 Bean 等等
    this.refreshBeanFactory();
    // 返回刚刚创建的 BeanFactory
    return this.getBeanFactory();
}
```
## refreshBeanFactory
```java
protected final void refreshBeanFactory() throws IllegalStateException
{
    if (!this.refreshed.compareAndSet(false, true))
    {
        throw new IllegalStateException("GenericApplicationContext does not support multiple refresh attempts: just call 'refresh' once");
    }
    else
    {
        this.beanFactory.setSerializationId(this.getId());
    }
}
```

