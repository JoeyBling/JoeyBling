---
title: SpringBoot配置文件中context-path不起作用
date: 2018-08-17 15:29
tags: Java
description: SpringBoot配置文件中context-path不起作用
---
#### SpringBoot 2.0.0.RELEASE版本后更新
- yml写法：
```java
server:
    servlet:
        context-path: /example
```

- properties写法：
```java
server.servlet.context-path=/example
```