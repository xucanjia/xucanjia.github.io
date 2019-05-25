---
layout: post
category: 技术
title: Python3打包exe
---

参考：
任务调度：https://lz5z.com/Python%E5%AE%9A%E6%97%B6%E4%BB%BB%E5%8A%A1%E7%9A%84%E5%AE%9E%E7%8E%B0%E6%96%B9%E5%BC%8F/
打包文件：
https://www.cnblogs.com/lizm166/p/8315468.html
```zsh
# 安装
pip install pyinstaller

#命令语法：pyinstaller -F 文件名（带后缀py）
#常用参数说明：
#–icon=图标路径
#-F 打包成一个exe文件
#-w 使用窗口，无控制台
#-c 使用控制台，无窗口
#-D 创建一个目录，里面包含exe以及其他一些依赖性文件
#pyinstaller -h 来查看参数

#将cmd的目录切换至（命令：cd 文件路径(注意空格)）需要打包的py文件目录下：
#有命令窗口弹出
pyinstaller -F shjys_rjjqk.py  
#无命令窗口弹出
pyinstaller -F -w shjys_rjjqk.py  
#或者
pyinstaller -F shjys_rjjqk.py  --noconsole

# my.ico 是一个图标名，和当前的shjys_rjjqk.py文件在同一个目录下
pyinstaller -F --icon=my.ico shjys_rjjqk.py  
```
```zsh
打包：生成exe（带参数）

　py中获取外界参数：

 　方法1：args 是运行前输入参数（不能在exe黑框中输入，可以用cmd窗口执行：shrjj.py 20180119）；
　 方法2：input是运行时输入参数（可以在exe黑框中输入）；
　 建议用input获取；
 　补充：方法一中的args参数（运行前输入参数）打包成exe，利用bat批处理来调用，传递参数；
 
注意：在有调用到外界配置文件的情况下，需要使用绝对路径；不然打包后，会出现找不到配置文件；
```