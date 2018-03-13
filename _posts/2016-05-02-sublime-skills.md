---
layout: post
category: ['sublime']
title: 关于sublime text的一些整理
---
# 新建PHP编译系统
`MAC`端

tools->build system->new bulid system

弹出的内容修改为如下
```php
{
    "cmd": ["php", "$file"],
    "file_regex": "php$",
    "selector": "source.php"
}
```

保存在默认的目录下即可,文件名为 `php.sublime-build`

直接运行当前xxx.php 文件  用快捷键 `ctrl+B` 可得结果


# SFTP 注册码
`SFTP-->setting user 填入下面这些`
```zsh
{  
    "email": "xiaosong@xiaosong.me",  
    "product_key": "d419f6-de89e9-0aae59-2acea1-07f92a"  
}  
-----------------------------------------------------------------------------------  
// {  
// "email":"Rimke@163.com",  
// "product_key":"e83eda-38644b-43c828-e3669b-cd8a85",  
// }  
```
# SFTP 设置
```zsh
{
    // The tab key will cycle through the settings when first created
    // Visit http://wbond.net/sublime_packages/sftp/settings for help
    
    // sftp, ftp or ftps
    "type": "sftp",

    "save_before_upload": true, // 上传前保存在本地
    "upload_on_save": true,     // 保存时同时上传
    "sync_down_on_open": true,  // 在本地打开服务器某个文件自动保存在本地
    "sync_skip_deletes": false,
    "sync_same_age": true,
    "confirm_downloads": false,
    "confirm_sync": true,
    "confirm_overwrite_newer": false,
    
    "host": "120.0.0.1",
    "user": "webuser",
    "password": "123456789",
    "port": "22", // 如是ftp改成21 注意和服务器设置的一致
    
    "remote_path": "服务器的项目目录(名字要一样)",
    "ignore_regexes": [
        "\\.sublime-(project|workspace)", "sftp-config(-alt\\d?)?\\.json",
        "sftp-settings\\.json", "/venv/", "\\.svn/", "\\.hg/", "\\.git/",
        "\\.bzr", "_darcs", "CVS", "\\.DS_Store", "Thumbs\\.db", "desktop\\.ini"
    ],
    //"file_permissions": "664",
    //"dir_permissions": "775",
    
    //"extra_list_connections": 0,

    "connect_timeout": 30,
    //"keepalive": 120,
    //"ftp_passive_mode": true,
    //"ftp_obey_passive_host": false,
    //"ssh_key_file": "~/.ssh/id_rsa",
    //"sftp_flags": ["-F", "/path/to/ssh_config"],
    
    //"preserve_modification_times": false,
    //"remote_time_offset_in_hours": 100, // 若不能上传 打开这个
    //"remote_encoding": "utf-8",
    //"remote_locale": "C",
    "allow_config_upload": false,
    
}

```