---
title: 解决MariaDB中文乱码
date: 2018-04-26 15:46
tags: Linux
description: 解决MariaDB中文乱码
---
#### 1.检查自己数据库编码
	# mysql -uroot -proot
	# show VARIABLES like 'char%';

![](https://upload-images.jianshu.io/upload_images/2743275-aed00e544adf23d4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<!--more-->
#### 2.更改Client和Server编码都是UTF-8

	# vim /etc/my.cnf.d/server.cnf
###### 在server.cnf中[mysqld]添加如下代码

	init-connect='SET NAMES utf8'  
	character-set-server = utf8

![](https://upload-images.jianshu.io/upload_images/2743275-109f93534d06e671.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###### 重启MariaDB即可
	# systemctl restart mariadb
	如果已经添加为服务
	# service mysqld restart