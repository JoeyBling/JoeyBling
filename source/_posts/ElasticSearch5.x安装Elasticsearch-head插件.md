---
title: ElasticSearch5.x安装Elasticsearch-head插件
date: 2018-08-21 16:03
tags: ELK日志分析平台
description: ElasticSearch5.x安装Elasticsearch-head插件
---
#### 一、安装Node.js环境
```shell
# cd /usr/local
# wget https://nodejs.org/dist/v8.11.4/node-v8.11.4-linux-x64.tar.xz
# yum install -y xz
# xz -d node-v8.11.4-linux-x64.tar.xz
# tar -xf node-v8.11.4-linux-x64.tar
# cd /usr/local/bin   //全局使用 npm 和 node,需要做相关软链
# ln -s /usr/local/node-v8.11.4-linux-x64/bin/node
# ln -s /usr/local/node-v8.11.4-linux-x64/bin/npm
# node -v
# npm -v
//使用淘宝镜像
# npm config get registry // https://registry.npmjs.org/
# npm config set registry https://registry.npm.taobao.org
```
<!--more-->
#### 二、下载插件包
去https://github.com/mobz/elasticsearch-head 下载代码上传到服务器上
```shell
# cd elasticsearch-head
# npm install -g grunt -cli
# npm install   //有报错忽略
# npm install grunt --save  //有报错忽略
# vim Gruntfile.js   // server.options增加 hostname: '0.0.0.0',
# vim _site/app.js  //修改ES端口与IP 默认为 http://localhost:9200
```
![](https://upload-images.jianshu.io/upload_images/2743275-10a0c4aae4bb3efb.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](https://upload-images.jianshu.io/upload_images/2743275-c94e1e6952bc69c4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 三、修改Elasticsearch配置
修改elasticsearch.yml文件加入以下内容：
```shell
# 是否支持跨域
http.cors.enabled: true
# *表示支持所有域名
http.cors.allow-origin: "*"
```
![](https://upload-images.jianshu.io/upload_images/2743275-68b0592e86fdf36f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
#### 四、重启Elasticsearch（一定要重启不然配置不生效）

#### 五、启动elasticsearch-head插件
```shell
# cd /usr/local/bin/
# ln -s /usr/local/node-v8.11.4-linux-x64/bin/grunt
# cd /usr/local/elasticsearch-5.5.2/elasticsearch-head
# grunt server (后台运行 + &)   
```
![](https://upload-images.jianshu.io/upload_images/2743275-38e4c25912195708.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/2743275-5f43e2a56b85e914.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
