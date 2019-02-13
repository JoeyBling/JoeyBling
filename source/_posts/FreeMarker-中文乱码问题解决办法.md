title: FreeMarker 中文乱码问题解决办法
tags: Java
description: Spring集成FreeMarker 中文乱码问题解决办法
date: 2018-04-17 15:53:54
---
解决办法一：通过修改配置文件freemarker.properties，修改默认编码：

	locale=zh_CN
	default_encoding=gbk
	number_format=#
	date_format=yyyy-MM-dd
	time_format=HH:mm:Ss
	datetime_format=yyyy-MM-dd HH:mm:Ss

还有1个办法   在contentType里设置value为text/html;charset=UTF-8"
<!--more-->
	<!-- FreeMarker视图解析器 -->
	<bean id="viewResolver"
		class="org.springframework.web.servlet.view.freemarker.FreeMarkerViewResolver">
		<property name="viewClass"
			value="org.springframework.web.servlet.view.freemarker.FreeMarkerView" />
		<property name="contentType" value="text/html;charset=UTF-8" />
		<property name="cache" value="false" />
		<property name="viewNames" value="*.ftl" />
		<property name="suffix" value="" />
		<property name="order" value="2" />
	</bean>

解决办法二：通过spring或其他第三方工具配置：

	<bean id="freemakerCongfig"
	    class="org.springframework.web.servlet.view.freemarker.FreeMarkerConfigurer">
	       <property name="templateLoaderPath">
		   <value>/WEB-INF/web/</value>
	       </property>
	       <property name="freemarkerSettings">
	       <props>
	       <prop key="defaultEncoding">gbk</prop>
	       </props>
	       </property>
	    </bean>


###### 页面编码和charset要跟上面配置的一致才可以，
	<meta http-equiv="Content-type" content="text/html; charset=gbk">

###### 注意：还有一种常见的导致乱码问题：编辑器或文件保存的编码和页面设置的编码不一致会导致乱码，例如文件的编码(用记事本打开,另存为可以看到文件的编码)为UTF-8而页面的charset=gbk就会出现乱码，反之也一样。