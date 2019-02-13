---
title: Linux 卸载分区
date: 2018-04-17 16:01:30
tags: Linux
description: Linux 卸载分区
---
##### 注意，卸载分区会格式化分区内所有的数据，请谨慎操作或进行数据备份
	# df -hT
![image.png](https://upload-images.jianshu.io/upload_images/2743275-d7fb0c77ed1e94d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<!--more-->    
	准备卸载/dev/sda6这个分区
	# umount /data2	
	重新检查一下 
	# df -hT
![image.png](https://upload-images.jianshu.io/upload_images/2743275-2af8caea924f6612.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	# fdisk -l
	发现待分区的磁盘 /dev/sda
![image.png](https://upload-images.jianshu.io/upload_images/2743275-c079a22b84557f0e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	对该磁盘进行卸载分区，输入m并回车
	# fdisk /dev/sda
	# m 输入帮助
	# p 打印分区表
![image.png](https://upload-images.jianshu.io/upload_images/2743275-85bcd2afce1808d7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/2743275-95439e347a38fcf6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

卸载/dev/sda6分区
此时注意/dev/sda6是刚刚卸载了/data2的分区名
![image.png](https://upload-images.jianshu.io/upload_images/2743275-d7fb0c77ed1e94d0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	# d 删除一个分区
	# 6  删除第六个分区
![image.png](https://upload-images.jianshu.io/upload_images/2743275-b7cbc678d5616a01.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	重新打印分区表发现已卸载/dev/sda6分区
	# p 
![image.png](https://upload-images.jianshu.io/upload_images/2743275-8969029b19517563.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

	# w   将表写入磁盘并退出
	再检查一遍
	# fdisk /dev/sda
	# p 打印分区表 
![image.png](https://upload-images.jianshu.io/upload_images/2743275-fc6779f38f7ccb43.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![image.png](https://upload-images.jianshu.io/upload_images/2743275-40d4fd8413ae4065.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
