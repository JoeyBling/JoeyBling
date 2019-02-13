title: Linux 查看网卡UUID
tags:
  - Linux
description: Linux 查看网卡UUID
categories: []
date: 2018-04-17 16:03:00
---
#### Linux 查看网卡UUID
###### 1、首先我们查看一下nmcli是哪个软件包提供的
	# yum provides "*/nmcli"
![image.png](https://upload-images.jianshu.io/upload_images/2743275-a42d314368eebd8e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<!--more-->
###### 2、安装NetworkManager服务
	# yum -y install NetworkManager

###### 3、启动NetworkManager服务
	# service NetworkManager start
![image.png](https://upload-images.jianshu.io/upload_images/2743275-21dd8cfcd7fc0216.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 4、查看网卡UUID
	# nmcli con
  	tips:如果有发现有报错
	# Error: could not connect to D-Bus.
	tips:查看/var/log/messages日志
	# vi /var/log/messages
	tips:按两下大写的G跳到最后一页
报错：

	...
	Apr 20 14:53:05 localhost NetworkManager[2013]: <info> NetworkManager (version 0.8.1-113.el6) is starting...
	Apr 20 14:53:05 localhost NetworkManager[2013]: <info> Read config file /etc/NetworkManager/NetworkManager.conf
	Apr 20 14:53:05 localhost NetworkManager[2013]: <error> [1492671185.606620] [nm-dbus-manager.c:278] nm_dbus_manager_init_bus(): Could not get the system bus.  Make sure the message bus daemon is running!  Message: Failed to connect to socket /var/run/dbus/system_bus_socket: Connection refused
	...
    
需要先启动messagebus，再启动NetworkManager

	# /etc/init.d/messagebus start
	tips:重新启动
	# service NetworkManager start
![image.png](https://upload-images.jianshu.io/upload_images/2743275-1d945ece865909ac.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### 运行nmcli
	# nmcli con
报错:
![image.png](https://upload-images.jianshu.io/upload_images/2743275-77a46ad27ca920e8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	查看/var/log/messages日志
	# vi /var/log/messages
发现有报错
![image.png](https://upload-images.jianshu.io/upload_images/2743275-8e47a7a12aeb9e68.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

###### g_slist_free_full 属于glist 的一个方法，缺少glist
###### 解决方法:
	# yum -y install glib2-devel
###### 3、此时再运行nmcli即可查看网卡UUID	
	# service NetworkManager start
	# nmcli con
![image.png](https://upload-images.jianshu.io/upload_images/2743275-ad3b6fb7812e01d8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)