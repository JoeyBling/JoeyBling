---
title: 新增Hexo博客文章置顶功能
date: 2019-02-25 11:40
tags: 日记本
description: 新增Hexo博客文章置顶功能
---
###### 修改Hexo文件夹下的node_modules/hexo-generator-index/lib/generator.js
需要添加的代码：
```javascript
posts.data = posts.data.sort(function(a, b) {
      if(a.top && b.top) {
          if(a.top == b.top) return b.date - a.date;
          else return b.top - a.top;
      }
      else if(a.top && !b.top) {
          return -1;
      }
      else if(!a.top && b.top) {
          return 1;
      }
      else return b.date - a.date;
  });
```
<!--more-->
以下是最终的generator.js内容：
```javascript
'use strict';

var pagination = require('hexo-pagination');

module.exports = function(locals) {
  var config = this.config;
  var posts = locals.posts.sort(config.index_generator.order_by);

  posts.data = posts.data.sort(function(a, b) {
      if(a.top && b.top) {
          if(a.top == b.top) return b.date - a.date;
          else return b.top - a.top;
      }
      else if(a.top && !b.top) {
          return -1;
      }
      else if(!a.top && b.top) {
          return 1;
      }
      else return b.date - a.date;
  });

  var paginationDir = config.pagination_dir || 'page';
  var path = config.index_generator.path || '';

  return pagination(path, posts, {
    perPage: config.index_generator.per_page,
    layout: ['index', 'archive'],
    format: paginationDir + '/%d/',
    data: {
      __index: true
    }
  });
};
```
----
如何使用：在需要置顶的文章添加top属性即可，排序从小到大![](https://upload-images.jianshu.io/upload_images/2743275-85427a7ca0fa1c91.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----
博客效果：![](https://upload-images.jianshu.io/upload_images/2743275-d3826b5a2d621b67.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

----
##### Tips:常用hexo命令
```bash
# hexo n == hexo new
# hexo g == 生成
# hexo s == 启动服务
```
