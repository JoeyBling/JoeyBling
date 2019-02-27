---
title: CentOS 6.X 安装VirtualBox-5.1
date: 2018-08-06 16:19
tags: Linux
description: CentOS 6.X 安装VirtualBox-5.1
---
##### 一、安装virtualbox的yum源
```shell
# vim /etc/yum.repos.d/virtualbox.repo
# 添加以下内容
[virtualbox] 
name=Oracle Linux / RHEL / CentOS-$releasever / $basearch - VirtualBox 
baseurl=http://download.virtualbox.org/virtualbox/rpm/el/$releasever/$basearch 
enabled=1 
gpgcheck=1 
gpgkey=http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc
```
<!--more-->
##### 二、添加EPEL源
```shell
# rpm -Uvh http://download.fedoraproject.org/pub/epel/6/i386/epel-release-6-8.noarch.rpm
```
##### 三、添加必要的依赖包
```shell
# yum install -y gcc make patch  dkms qt libgomp
# yum install -y kernel-headers kernel-devel fontforge binutils glibc-headers glibc-devel
# yum install -y kernel kernel-headers kernel-devel gcc make
```
##### 四、设置环境变量，主要是内核的路径
```shell
# vim /etc/profile
# 文件最后行添加
export KERN_DIR=/usr/src/kernels/你的最新内核版本xxx
# source /etc/profile
```
##### 五、安装virtualbox
```shell
# yum search VirtualBox
# yum install -y VirtualBox-5.1
# reboot
# 重新编译与virtualbox相关的内核模块
# service vboxdrv setup
# 启动virtualbox
# virtualbox &
```
![](https://upload-images.jianshu.io/upload_images/2743275-6c0e7cf6fbadb6f8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

