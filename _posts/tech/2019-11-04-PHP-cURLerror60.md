---
layout: post
category: 技术
title: cURL error 60
tags: PHP
---
# 报错信息：

```zsh
cURL error 60: SSL certificate problem: unable to get local issuer certific   ate (see http://curl.haxx.se/libcurl/c/libcurl-errors.html)
```

## 解决方法：

要解决此错误，需要定义CURL证书颁发机构信息路径
要做到些,

`在这里下载最新的curl认可证书: https://curl.haxx.se/ca/cacert.pem`

保存cacert.pem文件在一个可以引入的目录。

然后，在php.ini文件中，向下滚动到找到[curl]的位置。

您应该看到CURLOPT_CAINFO选项被注释掉了。取消注释并指向cacert.pem文件。你应该有这样一行:
```zsh
curl.cainfo = “证书目录\cacert.pem”
```
保存并关闭php.ini。重新启动web服务器并再次尝试您的请求。
如果没有设置正确的位置，将会得到`CURL 77`错误。
```zsh
cURL error 77: error setting certificate verify locations:
    CAfile: certificate D:\phpStudy\PHPTutorial\php\php-7.2.1-nts\extras\ssl\
  cacert.pem
    CApath: none (see http://curl.haxx.se/libcurl/c/libcurl-errors.html)
```
