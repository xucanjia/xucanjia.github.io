---
layout: post
category: 技术
title: SSL配置
---

## phpstudy 配置 ssl证书
1.打开 php扩展  →  php-openssl

2.修改httpd.conf文件
    a.去掉    `LoadModule ssl_module modules/mod_ssl.so` 前面的 `#`
    b.去掉    `Include conf/extra/httpd-ssl.conf` 前面的 `#`

3.复制SSL证书文件到指定目录
 phpStudy/Apache/conf/sssl 目录下。是 `sssl` 目录,`需要新建的,ssl文件夹是原来就有的`。

4.配置

打开目录 phpStudy/Apache/conf/extra找到 `httpd-ssl.conf`文件。打开该文件。

`如果你安装在c盘,可以全部清除复制以下代码,根据你项目的地址来`
```zsh
Listen 443
<VirtualHost *:443>
    DocumentRoot "C:\phpStudy\PHPTutorial\WWW\yii2\web"
    ServerName xxxx.com
    ServerAlias xxxx.com
    SSLEngine on
    SSLProtocol TLSv1 TLSv1.1 TLSv1.2
    SSLCipherSuite HIGH:MEDIUM:!aNULL:!MD5
    SSLCertificateFile "C:\phpStudy\PHPTutorial\Apache\conf\sssl\2_fqwlkj.cn.crt"
    SSLCertificateKeyFile "C:\phpStudy\PHPTutorial\Apache\conf\sssl\3_fqwlkj.cn.key"
    SSLCertificateChainFile "C:\phpStudy\PHPTutorial\Apache\conf\sssl\1_root_bundle.crt"
    <Directory "C:\phpStudy\PHPTutorial\WWW\yii2\web">
      Options +Indexes +FollowSymLinks +ExecCGI
      AllowOverride All
      Order allow,deny
      Allow from all
      Require all granted
  </Directory>
</VirtualHost>
```