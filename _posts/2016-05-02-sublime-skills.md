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


