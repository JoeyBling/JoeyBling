---
title: Linux临时和永久关闭selinux
date: 2018-08-02 14:26
tags: Linux
description: Linux临时和永久关闭selinux
---
#### 临时关闭：
```shell
# setenforce 0
```
#### 永久关闭：
```shell
# vim /etc/sysconfig/selinux
```
SELINUX=enforcing 改为 SELINUX=disabled

重启服务reboot