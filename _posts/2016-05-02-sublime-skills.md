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