---
title: Linux下Tomcat指定JDK和设置内存大小
date: 2018-08-06 17:57
tags: Linux
description: Linux下Tomcat指定JDK和设置内存大小
---
##### 一、Linux下Tomcat指定JDK
```shell
# vim bin/setclasspath.sh
```
在脚本开头的地方指定JAVA_HOME和JRE_HOME
```shell
export JAVA_HOME=/usr/local/jdk1.8.0_40
export JRE_HOME=/usr/local/jdk1.8.0_40/jre
```
<!--more-->
##### 二、Linux下Tomcat设置内存大小
```shell
# vim bin/catalina.sh
```
###### Tomcat设置内存为8G:JAVA_OPTS="-server -Xms8192M -Xmx8192M -XX:PermSize=256M -XX:MaxPermSize=256M"

###### Tomcat设置内存为4G:JAVA_OPTS="-server -Xms4096M -Xmx4096M -XX:PermSize=256M -XX:MaxPermSize=256M"
![](https://upload-images.jianshu.io/upload_images/2743275-af5bcc478597a94a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
