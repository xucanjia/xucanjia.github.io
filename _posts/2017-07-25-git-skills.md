---
layout: post
category: ['git']
title: Windows Server 搭建 git服务器
---

先看下过程:

![过程](http://oi2atwmcz.bkt.clouddn.com/gitblit.png)

# 1.准备工作
 * `下载Java运行环境:` <http://www.java.com/zh_CN/>  注意自己的服务器32位还是64位
 	*下载内容: `JRE` 和 `JDK`

 * `下载Gitblit:` <http://www.gitblit.com/>  下载Windows版


# 2.安装及配置

### 安装Java环境及配置

1.安装JRE和JDK,可更改自己想要安装的目录,`但是记得保存在同一个目录之下`

![](http://oi2atwmcz.bkt.clouddn.com/javashow.png)

2.配置Java环境变量:
* 右键” 计算机” => ”属性” => ”高级系统设置” => ”高级” => “环境变量” => `“系统变量”`。

* 新建: 变量名: JAVA_HOME；变量值: `C:\Program Files\Java\jdk1.8.0_144`

* `注意`: 变量值是 JDK的目录

* 新建: 变量名: CLASSPATH；变量值: `%JAVA_HOME%/lib/dt.jar;%JAVA_HOME%/lib/tools.jar`

* 添加: 找到PATH变量, 选择编辑。把 `%JAVA_HOME%/bin;%JAVA_HOME%/jre/bin` 添加到”变量值”的结尾处。


3.验证是否安装成功
* 命令行输入 javac 若出现下图则代表安装成功

* ![](http://oi2atwmcz.bkt.clouddn.com/javasuccess.png)

* 提示不是内部或者外部命令,原因可能是`Java环境变量配置出错`,或者 `没有安装 JDK`


### 安装Gitblit
1.无需安装,解压Gitblit到你想放置的位置

2.创建用于存储项目代码的文件夹。这里为C:\GitProject

3.配置Gitblit:

* Gitblit目录下,进入 data 找到 `defaults.properties`
* git.repositoriesFolder(资料库路径), 赋值为C:/GitProject/ 注意:这里是 `/` 而不是 `\`
* 找到 `server.httpPort`, 设定http协议的端口号,改为 server.httpPort = 10101 (端口号自定)
* 找到 `server.httpBindInterface`, 设定`服务器的IP地址`。这里就设定你的`服务器IP`,注意是`电脑IP地址`
* 找到`server.httpsBindInterface`, 设定为localhost
* 找到`server.shutdownPort` , 其默认值为 8081, 是否被占用, 如果占用请修改

4.Gitblit目录下 管理员身份运行 `gitblit.cmd`,若出现下图,则代表成功

![](http://oi2atwmcz.bkt.clouddn.com/gitsuccess.png)

* 若失败,则检查配置是否配置正确,尤其服务器的IP地址,注意是`电脑IP地址`,命令行中输入 ipconfig 可看见

5.设置开机启动

* 打开installService.md
* 设置 SET ARCH=amd64（64位, 32位机器为 x86）
* 设置 SET CD=C:\Program Files\gitblit-1.8.0, 值为gitblit的路径
* 将启动参数设为空值, 采用默认的参数即可 , --StartParams="" ^
* 确保开启启动,在进入`服务`中,查看gitblit是否为自动模式
* ![](http://oi2atwmcz.bkt.clouddn.com/gitset.png)



# 3.glitblit的使用
### 在浏览器中输入: http://172.*.*.*:10101/ ,默认可以用admin和admin进行登录, 然后改密即可。
* 浏览器会禁用Javascript脚本运行,请在Internet属性中->安全->自定义级别->脚本->启用 `java小程序脚本` 和 `活动脚本`
* 添加几个用户或者团队,根据项目开发人员而定
### 创建版本库

假设创建tdatda版本库

* ![](http://oi2atwmcz.bkt.clouddn.com/girpro.png)
* 这时候,版本库已经创建好了,可到 存储项目代码的文件夹查看,这里为C:\GitProject
* `这时候还没有项目的文件`,需要自动部署文件,需要`指定一个文件夹`
* gitblit 所有hook(钩子)都放在这个目录 C:\gitblit\data\groovy (看你gitblit放在哪)
* 把localclone.groovy复制另存为 autotest.troovy
* 修改autotest.troovy中的

```bash
	def rootFolder = 'c:/test'
	#修改为
	def rootFolder = 'C:/phpStudy/WWW/test' `这里用的是phpstudy,所以就放在WWW目录中,这里是测试我又新建了test目录`
```
rootFolder：自动部署  根目录

![](http://oi2atwmcz.bkt.clouddn.com/gitfloder.png)

### 编辑配置版本库,比如:已经创建了 `tdatda`
1.版本库

![](http://oi2atwmcz.bkt.clouddn.com/ddd.png)

2.点击 编辑 找到刚刚的 hook   保存

![](http://oi2atwmcz.bkt.clouddn.com/gitedit.png)



# 4.Coding...

1.首先,访问gitblit服务器

http://`39.39.*.*:10101`  红色部分为服务器地址

2.用账号登录(就是gitblit中注册的用户)

3.版本库

![](http://oi2atwmcz.bkt.clouddn.com/ssdf.png)

`复制为SourceTree克隆准备的URL`

4.在本地SourceTree客户端

新建仓库->从URL克隆

粘贴 http://zao@39.xx8.xx6.128:10101/r/tdatda.git

注意:`这里是你服务器的地址`,端口记得防火墙入站规则要开

若提示这不是一个有效的路径,则把  `.git` 去掉, 至于为什么有时候会这样,我也没弄明白

![](http://oi2atwmcz.bkt.clouddn.com/sttu.png)

这时候,目录里只有一个初始化的目录

![](http://oi2atwmcz.bkt.clouddn.com/suut.png)

紧接着就是项目的管理者上传第一份文件了

gitblit服务器端中  我们设置的hook 会自动部署文件

我的是在`C:/phpStudy/WWW/test`

![](http://oi2atwmcz.bkt.clouddn.com/tdatad.png)


参考:

<https://wenku.baidu.com/view/49b434269ec3d5bbfc0a7497.html>



