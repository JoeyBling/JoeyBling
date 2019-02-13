title: CentOS6.5 离线安装MySQL5.6.26
tags: Linux
description: CentOS6.5 离线安装MySQL5.6.26
date: 2018-06-06 15:59:52
---
#### 1、卸载之前安装的MySQL
```shell
# rpm -qa | grep mysql   --查看系统之前是否已安装MySQL。
# rpm -e --nodeps mysql-libs-5.1.71-1.el6.x86_64   --执行删除语句
# rm -rf /var/lib/mysql*   --善后处理
# rm -rf /usr/share/mysql*
```
<!--more-->
#### 2、安装MySQL
###### 2.1 下载并安装 libaio
```shell
# cd /usr/local
# wget http://mirror.centos.org/centos/6/os/x86_64/Packages/libaio-0.3.107-10.el6.x86_64.rpm
# rpm -ivh libaio-0.3.107-10.el6.x86_64.rpm
```
###### 2.2 下载并安装MySQL
```shell
# cd /usr/local
# wget https://dev.mysql.com/get/archives/mysql-5.6/MySQL-5.6.26-1.linux_glibc2.5.x86_64.rpm-bundle.tar
# tar -xf MySQL-5.6.26-1.linux_glibc2.5.x86_64.rpm-bundle.tar
# rpm -ivh MySQL-server-5.6.26-1.linux_glibc2.5.x86_64.rpm
# rpm -ivh MySQL-client-5.6.26-1.linux_glibc2.5.x86_64.rpm
```
###### 2.3 查看并修改MySQL root用户密码
```shell
# more /root/.mysql_secret
# service mysql restart
# mysqladmin -uroot -pFeyU2YjwMcAw9Nv0 password 'root'  --修改root密码为root
# mysql -uroot -proot   --测试登陆
```
![](https://upload-images.jianshu.io/upload_images/2743275-1d296e2cb8b73d3c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
###### 2.4 配置MySQL数据库编码
```shell
# cp -rp /usr/share/mysql/my-default.cnf /etc/my.cnf
# 在mysqld下面增加
init-connect='SET NAMES utf8'
character-set-server = utf8
# service mysql restart
# mysql -uroot -proot  --验证是否成功
# show variables like 'character%';
```
![](https://upload-images.jianshu.io/upload_images/2743275-6cdfd951579ad2d3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

------------
![](https://upload-images.jianshu.io/upload_images/2743275-eb169140eb6b5b36.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


###### 2.5 配置MySQL远程访问
```shell
# service iptables stop
# chkconfig iptables off
# mysql -uroot -proot
# grant all privileges on *.* to root@'%' identified by 'root' WITH GRANT OPTION;
# flush privileges;
```