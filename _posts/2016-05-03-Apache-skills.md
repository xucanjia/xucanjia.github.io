---
layout: post
category: ['Apache']
title: Apache 安装配置
---

## TODO(安装)

## 配置本地虚拟域名

执行~
```bash
subl /private/etc/hosts
```
`分配几个域名`
```bash
127.0.0.1	localhost

127.0.0.1	bb.test

127.0.0.1	bb.cn

127.0.0.1	cc.cn

127.0.0.1	cc.test
```

## 指向项目
执行~
```bash
subl /usr/local/etc/apache2/2.4/extra/httpd-vhosts.conf
```
`底部增加`

```bash
<VirtualHost *:80>
    ServerName cc.test
    ServerAlias cc.cn
    DocumentRoot "/Users/apple/home/wwwroot/cc/backend/web"
    <Directory "/Users/apple/home/wwwroot/cc/backend/web">
        Options Indexes FollowSymLinks
        Require all granted
        AllowOverride All
        <IfModule mod_rewrite.c>
            RewriteEngine On
            RewriteCond %{REQUEST_FILENAME} !-f
            RewriteCond %{REQUEST_FILENAME} !-d
            RewriteRule ^(.*)$ /index.php/$1 [L]
        </IfModule>
    </Directory>
</VirtualHost>
```
