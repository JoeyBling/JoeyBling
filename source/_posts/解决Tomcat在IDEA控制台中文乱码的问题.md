---
title: 解决Tomcat在IDEA控制台中文乱码的问题
date: 2019-02-18 14:01
tags: 日记本
description: 解决Tomcat在IDEA控制台中文乱码的问题
---
###### 在idea的安装目录下的bin/idea.exe.vmoptions文件和idea64.exe.vmoptions文件的末尾另起一行添加
```shell
-Dfile.encoding=UTF-8
```
![](https://upload-images.jianshu.io/upload_images/2743275-61972ac0c4df530b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
