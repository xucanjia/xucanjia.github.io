---
layout: post
title: 微信开发
category: 技术
tags: wechat
description: 一些常用的方法
---
### 微信网页标题设置
```js
  var $body = $('body');  
  document.title = '附近商家优惠'  // hack在微信等webview中无法修改document.title的情况
  var $iframe = $('<iframe src="/favicon.ico"></iframe>').on('load', function() {     
     setTimeout(function() {
         $iframe.off('load').remove()   
     }, 0)
  }).appendTo($body)
```

