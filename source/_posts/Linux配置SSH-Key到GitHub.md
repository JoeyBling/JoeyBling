title: Linux配置SSH Key到GitHub
tags: Linux
date: 2018-04-17 14:48:40
---
#### 1.生成SSH Key
首先检查下本机是否已经安装了SSH，在终端输入ssh即可： 
![](https://upload-images.jianshu.io/upload_images/2743275-d5ee041fc6a3b53e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
如果没有安装进行yum安装

<!--more-->

	# yum -y install openssh-clients

###### 接下来就是生成ssh key了，输入ssh-keygen -t rsa，然后连续按回车键三次（注意：千万不要输入密码！）。
![](https://upload-images.jianshu.io/upload_images/2743275-7398d3f9f1eef72c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
id_rsa.pub为公钥，id_rsa为私钥，它们都是隐藏文件。
那么如何查看它们的内容呢？只需要继续执行以下两条命令即可。

	# cd .ssh/
	# cat id_rsa.pub
![](https://upload-images.jianshu.io/upload_images/2743275-2c142d50f896e48b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#### 2.添加SSH Key到GitHub上
![](https://upload-images.jianshu.io/upload_images/2743275-062ea02946eb9af5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
接着执行下面操作： 
![](https://upload-images.jianshu.io/upload_images/2743275-d2a6a8697131e8d7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
点击New SSH Key按钮后进行Key的填写操作，完成SSH Key的添加。如下图： 
![](https://upload-images.jianshu.io/upload_images/2743275-1a8f4cd790d9d667.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/2743275-cdbdf7fd81c8ac11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
添加SSH Key成功之后，继续输入命令进行测试。

	# ssh -T git@github.com
![](https://upload-images.jianshu.io/upload_images/2743275-5310d1ab738cb79a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

出现上图结果则说明添加SSH Key成功。