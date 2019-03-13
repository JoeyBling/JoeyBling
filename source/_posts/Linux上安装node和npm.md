---
title: Linux上安装node和npm
date: 2018-04-20 15:31
tags: Linux
description: Linux上安装node和npm
---
#### 一、下载Node

  官网下载链接：https://nodejs.org/zh-cn/download/
![](https://upload-images.jianshu.io/upload_images/2743275-497a8e6f4e7c11d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

<!--more-->
解压目录
```
# yum install -y xz
# xz -d node-v8.11.1-linux-x64.tar.xz
# tar -xf node-v8.11.1-linux-x64.tar
```

这里想要全局使用npm 和 node,就需要做相关软链，如下！
```
# cd /usr/local/bin
# ln -s /usr/local/src/node-v8.10.0-linux-x64/bin/npm
# ln -s /usr/local/src/node-v8.10.0-linux-x64/bin/node
```

然后即可在任意位置执行 node  -v   npm  -v  查看相应的版本，则安装完成！

#### 二、使用淘宝镜像
```
# npm config get registry // https://registry.npmjs.org/
# npm config set registry https://registry.npm.taobao.org
```
