---
title: Linux下同步网络时间
tags: Linux
description: Linux下同步网络时间
date: 2018-08-11 01:17:15
---
#### 一、安装ntp
```shell
# yum install -y ntpdate
```
#### 二、同步时间
```shell
# 方式一、使用域名连接，要经过DNS解析，速度慢。
# ntpdate pool.ntp.org
# 方式二、使用IP连接，超级快。
# ntpdate 120.24.81.91
```
