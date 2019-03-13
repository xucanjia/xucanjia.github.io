---
layout: post
category: 工具
title: 常用命令
---
### 本机的网络连接

```zsh
netstat -anop tcp

netstat -an
```
```zsh
CLOSED 表示socket连接没被使用。
LISTENING 表示正在监听进入的连接。
SYN_SENT 表示正在试着建立连接。
SYN_RECEIVED 进行连接初始同步。
ESTABLISHED 表示连接已被建立。
CLOSE_WAIT 表示远程计算器关闭连接，正在等待socket连接的关闭。
FIN_WAIT_1 表示socket连接关闭，正在关闭连接。
CLOSING 先关闭本地socket连接，然后关闭远程socket连接，最后等待确认信息。
LAST_ACK 远程计算器关闭后，等待确认信号。
FIN_WAIT_2 socket连接关闭后，等待来自远程计算器的关闭信号。
TIME_WAIT 连接关闭后，等待远程计算器关闭重发。
```
线上大量CLOSE_WAIT分析:

<https://dayutalk.cn/2018/12/08/%E7%BA%BF%E4%B8%8A%E5%A4%A7%E9%87%8FCLOSE_WAIT%E5%88%86%E6%9E%90/>