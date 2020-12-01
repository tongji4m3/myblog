---
title: docker常用命令与使用
author: tongji4m3
top: false
cover: false
coverImg: /images/1.jpg
toc: true
mathjax: false
summary: '一些常用工具的笔记,主要写了docker常用命令与使用'
categories: 常用工具
tags:
  - 工具
  - Docker
abbrlink: 65fb0b69
date: 2020-07-19 00:00:00
---





# Docker理解

1. docker对进程进行隔离,将软件所需的所有资源打包到一个隔离的容器中.

2. 容器是相互隔离的,每个容器内部都有一个属于自己的文件系统

3. 镜像与容器。容器是用镜像创建的运行实例。容器可以看作简易版的Linux环境

4. 仓库包含多个镜像，每个镜像都有不同的标签（tag），即版本

5. 联合文件系统:一些已经下的基础包就不会继续下了

6. 帮助命令:`docker --help`

7. > Docker容器卷
  >
  > 容器之间共享数据
  >
  > docker run -it -v 宿主机目录:容器内目录 镜像名 

# 镜像命令 
> 
	> docker images                查看镜像
	>
	> docker search  镜像名
	>
	> docker pull 镜像名[:TAG]          不写TAG则默认下最新版本
	>
	> docker rmi -f 镜像名[:TAG]            删除镜像
	>
	> docker rmi -f $(docker images -qa)  删除全部镜像

​	
# 容器命令                              

> docker run -it  --name centos1  镜像ID/镜像名 
>
> docker ps              参数-a,列出历史上所有运行过的
>
> docker stop 容器ID 
>
> docker start 容器ID    
>
> docker rm 容器ID    删除已停止的容器 参数-f 强制删除正在运行的容器
>
> docker run -d    镜像ID 以守护式启动,后台运行  如果该进程没有前台进程,会自动退出
>
> exit 直接退出docker容器
>
> docker exec -it centos1 /bin/bash 重新进入当前运行的 容器
>
> docker run -it  -p 8888:8080 tomcat 带端口的启动
>
> docker run  -it --name centos7 centos:7   /bin/bash 
>
> docker logs -f -t  --tail 10  centos7  **-f :** 跟踪日志输出  **-t :** 显示时间戳
>
> docker top centos7 查看容器内进程信息
>
> docker inspect centos7 查看容器内具体信息
>
> docker cp centos7:/usr/tongji4m3.txt . 拷贝容器内文件到主机
>
> 
>
> --name="名称" 容器名
>
> -d 后台运行
>
> -it 以交互方式运行,进入容器
>
> -p 8888:8080  指定端口映射

# DockerFile创建容器
首先新建个文件`vim DockerFile`

```c
	FROM centos

    ENV mypath /usr/local
	WORKDIR $mypath
    
    RUN yum -y install vim
    
    EXPOSE 80
	CMD /bin/bash
```

创建  `docker build -f /root/myDocker/DockerFile -t mycentos:1.0 .`

之后就可以正常使用：`docker run -it mycentos:1.0`



# 常用软件安装

## redis

### 安装

```docker run -d --name redis -p 6379:6379 redis --requirepass "redis"```

### 以客户端启动

```docker exec -it redis redis-cli -a redis ```

# 一些例子

```javascript
FROM centos
#拷贝宿主机的文件到容器的文件
COPY temp.txt /usr/local/container.txt
#把Java，tomcat添加到容器中
ADD jdk-8u221-linux-x64.tar.gz /usr/local/
ADD apache-tomcat-9.0.8.tar.gz /usr/local/
#安装vim编辑器
RUN yum -y install vim
#设置登录落脚点
ENV MYPATH /usr/local
WORKDIR $MYPATH
#配置Java，tomcat环境变量
ENV JAVA_HOME /usr/local/jdk1.8.0.221
ENV CLASSPATH $JAVA_HOME/lib/dt.jar
#配置java与tomcat环境变量
ENV JAVA HOME /usr/1ocal/jdk1.8.0_ 171
ENV CLASSPATH $JAVA_HOME/1ib/dt.jar: $JAVA_HOME/lib/tools.jar
ENV CATALINA_HOME /usr/local/apache-tomcat-9.0.8
ENV CATALINA_BASE /usr/local/apache-tomcat-9.0.8
ENV PATH $PATH: $JAVA_HOME/bin:$CATALINA_HOME/lib:$CATALINA_HOME/bin
#监听窗口
EXPOSE 8080
#启动时运行tomcat
CMD /usr/local/apache-tomcat-9.0.8/bin/startup.sh

    
```



`docker pull mysql:5.7`

> mysql安装
>
> docker run -p 3306:3306 --name mysql -v /root/mysql/conf:/etc/mysql/conf.d -e MYSQL_ROOT_PASSWORD=root -d mysql:5.7

启动:

`docker exec -it mysql bash`

`mysql -uroot -proot`