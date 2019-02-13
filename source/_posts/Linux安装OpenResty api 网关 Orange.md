title: Linux安装OpenResty api 网关 Orange
tags: Linux
description: Linux安装OpenResty api 网关 Orange
date: 2018-06-05 15:57:03
---
#### 1.安装openresty
```shell
# yum -y install libuuid-devel pcre-devel openssl-devel gcc-c++ wget
# mkdir /openresty
# cd /openresty
# wget https://openresty.org/download/openresty-1.9.15.1.tar.gz
# tar -zxf openresty-1.9.15.1.tar.gz
# cd openresty-1.9.15.1
# ./configure --with-http_stub_status_module --with-http_v2_module --with-http_ssl_module 
# gmake && gmake install
# ln -s /usr/local/openresty/nginx/sbin/nginx /usr/sbin/nginx
# nginx -v
```
<!--more-->
#### 2.创建MySQL数据库并导入数据(脚本在orange/install文件夹下)
```shell
# yum -y install mariadb-server
# mysql -u root
# CREATE DATABASE orange CHARACTER SET utf8 COLLATE utf8_general_ci;
# CREATE USER 'orange'@'%' IDENTIFIED BY 'orange';
# GRANT ALL PRIVILEGES ON orange.* TO 'orange'@'%';
# FLUSH PRIVILEGES;
# 最后一定要执行mysql的数据库导入。
# mysql -u orange -porange -h 10.0.2.15 orange < orange-v0.6.2.sql
```
#### 3.安装Orange
###### 安装之前需要 lor 框架，否则启动有问题。
```shell
# yum install -y git
# git clone https://github.com/sumory/lor.git
# cd lor
# make install
```
###### 启动并配置 orange 服务
```shell
# service iptables stop
# chkconfig iptables off
# git clone https://github.com/sumory/orange.git
# cd orange
# vim conf/orange.conf
# sh start.sh
```
![](https://upload-images.jianshu.io/upload_images/2743275-2e009409e9d775d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


##### 访问地址: http://IP:9999
![](https://upload-images.jianshu.io/upload_images/2743275-b87cf50db17bdbf6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### Tips:启动不起来查看端口占用情况杀掉其他进程
```shell
# netstat -tunlp |grep 80
```