---
title: ELK之本地Grok Debugger配置
date: 2018-04-15 08:13:52
tags: ELK日志分析
---
1、Ruby环境安装

	清理已安装过的
	#yum erase ruby ruby-libs ruby-mode ruby-rdoc ruby-irb ruby-ri ruby-docs
	#yum remove ruby

	1.Ruby的安装
	#yum install -y wget unzip
	#cd /usr/local
	#yum -y install  openssl-devel gcc
	#wget https://ruby.taobao.org/mirrors/ruby/2.1/ruby-2.1.7.tar.gz
	#tar zxf ruby-2.1.7.tar.gz
	#cd ruby-2.1.7
	#./configure --prefix=/usr/local/ruby2.1.7
	#make && make install
	#echo 'export PATH=/usr/local/ruby2.1.7/bin:$PATH'>>/etc/profile
	#source /etc/profile
	说明：别使用ruby最新的2.2或者2.3的版本，可能出现部分组件无法安装
<!--more-->
	2. RubyGems工具安装
	#cd /usr/local
	#wget http://rubygems.global.ssl.fastly.net/rubygems/rubygems-2.6.2.tgz
	#tar zxf rubygems-2.6.2.tgz
	#cd rubygems-2.6.2
	#ruby setup.rb

	3.替换gem源,又是由于网络环境的问题，访问官方源非常慢，使用淘宝的gem源
	#gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
	#gem sources –l

	4.Grokbug的安装
	#mkdir /usr/local/grokbug
	#cd /usr/local/grokbug
	#wget https://codeload.github.com/nickethier/grokdebug/zip/master
	#unzip master
	#mv grokdebug-master/* .
	#rm -rf grokdebug-master/

	5.Ruby组件安装(以下组件都对版本有相应的要求)
	查看缺少的组件
	#ruby config.ru
	就会提示组件及对应的版本
	#gem install bundler
	gem install cabin -v=0.5.0
	gem install haml -v=3.1.7
	gem install jls-grok -v=0.10.10
	gem install json -v=1.7.5
	gem install kgio -v=2.8.0
	gem install rack -v=1.4.1
	gem install rack-protection -v=1.2.0
	gem install raindrops -v=0.11.0
	gem install shotgun -v=0.9
	gem install tilt -v=1.3.3
	gem install sinatra -v=1.3.3
	gem install unicorn -v=4.6.3

	6.启动服务
	#cd /usr/local/grokbug
	#nohup bundle exec unicorn -p 8080 -c ./unicorn &

	7.关闭防火墙
	#service iptables stop
	#chkconfig iptables off

	8.替换Google的jquery源
	#cd /usr/local/grokbug
	#cd views 

###执行下面5条语句

	sed -i 's#//ajax.googleapis.com/ajax/libs/jquery/1.8.1/jquery.min.js#//lib.sinaapp.com/js/jquery/1.8.1/jquery.min.js#g' index.haml

	sed -i 's#//ajax.googleapis.com/ajax/libs/jqueryui/1.9.2/jquery-ui.min.js#//lib.sinaapp.com/js/jquery-ui/1.9.2/jquery-ui.min.js#g' index.haml

	sed -i 's#//ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js#//lib.sinaapp.com/js/jquery/1.7.2/jquery.min.js#g' patterns.haml

	sed -i 's#//ajax.googleapis.com/ajax/libs/jqueryui/1.9.0/themes/ui-lightness/jquery-ui.css#//lib.sinaapp.com/js/jquery-ui/1.9.0/themes/ui-lightness/jquery-ui.css#g' layout.haml

	sed -i 's#//ajax.googleapis.com/ajax/libs/jquery/1.7.2/jquery.min.js#//lib.sinaapp.com/js/jquery/1.7.2/jquery.min.js#g' discover.haml


测试，通过web路径访问测试了
[http://xxx](http://master.am.com/ambari):8080

![](https://upload-images.jianshu.io/upload_images/2743275-ab527d48b90f29e8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



