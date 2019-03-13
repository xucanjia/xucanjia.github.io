---
layout: post
category: 技术
title: redis环境搭建(Mac端)
---
## 安装
#### 1.官网下载:<http://redis.io/>

#### 2.将下载下来的tar.gz 压缩包拷贝到usr/local目录下
```zsh
sudo cp redis-3.2.8.tar.gz /usr/local
```
#### 3.cd /usr/local文件夹中,解压该压缩文件
```zsh
sudo tar -zxf redis-3.2.8.tar.gz
```
#### 4.编译测试
```zsh
sudo make test
```
出现 `\o/ All tests passed without errors!` 继续下一步.

#### 5.redis安装:
```zsh
sudo make install
```
至此,安装已完成、不过还需将redis配置一下


安装完Redis后，在终端中输入：
```zsh
redis-server
```
即可启动Redis服务。

要关闭Redis服务也很简单，先用Redis客户端连上Redis服务，
```zsh
redis-cli
```
用SHUTDOWN命令即可关闭服务。
```zsh
SHUTDOWN
```
