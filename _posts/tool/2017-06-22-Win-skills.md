---
layout: post
category: 工具
title: Win常用的
---
## Win命令行提示 `php不是内部或外部命令`

环境变量设置下，要把php的执行文件,也就是php.exe设置到环境变量里面

我的电脑->属性->高级->环境变量设置->PATH->编辑->在后面添加一个到php.exe的路径就可以了。

如安装在 (`c:\phpstudy\PHP\php5.4.12`) 复制这个地址 记得前面加  `;`
![如](http://oi2atwmcz.bkt.clouddn.com/WechatIMG4903.jpeg)


## windows下修改host不生效的或者hosts空白或者不存在
hosts不存在 直接新建一个 复制如下
```zsh
# Copyright (c) 1993-1999 Microsoft Corp.
#
# This is a sample HOSTS file used by Microsoft TCP/IP for Windows.
#
# This file contains the mappings of IP addresses to host names. Each
# entry should be kept on an individual line. The IP address should
# be placed in the first column followed by the corresponding host name.
# The IP address and the host name should be separated by at least one
# space.
#
# Additionally, comments (such as these) may be inserted on individual
# lines or following the machine name denoted by a '#' symbol.
#
# For example:
#
# 102.54.94.97 rhino.acme.com # source server
# 38.25.63.10 x.acme.com # x client host

127.0.0.1 lmlicenses.wip4.adobe.com
127.0.0.1 lm.licenses.adobe.com

127.0.0.1 localhost
127.0.0.1 tp.test
127.0.0.1 www.tp.test
127.0.0.1 tt.test
127.0.0.1 dd.test
127.0.0.1 cc.test
127.0.0.1 bb.test
127.0.0.1 aa.test
```
`由于电脑系统是第三方一键重装的，导致hosts不生效或者空白`

设置apache虚拟域名的时候不生效，网上找了方法，记录一下。

1.检查网络情况
  ping aa.test 检查是不是127.0.0.1 发出的 是的话是apache配置问题
2.重指host文件（C:\Windows\System32\drivers\etc）

->打开本地连接->更改适配器->右击属性->Internet 协议版本4->属性->高级

->选择WINS->勾选 启用LMHOSTS->导入LMHOSTS->选择hosts->确定完成

查看：

命令行(cmd)运行:ipconfig /flushdns #清除DNS缓存内容。

ps:ipconfig /displaydns //显示DNS缓存内容
