---
layout: post
category: 技术
title: 关于sublime text的一些整理
---
# 注册码
```zsh
----- BEGIN LICENSE -----
sgbteam
Single User License
EA7E-1153259
8891CBB9 F1513E4F 1A3405C1 A865D53F
115F202E 7B91AB2D 0D2A40ED 352B269B
76E84F0B CD69BFC7 59F2DFEF E267328F
215652A3 E88F9D8F 4C38E3BA 5B2DAAE4
969624E7 DC9CD4D5 717FB40C 1B9738CF
20B3C4F1 E917B5B3 87C38D9C ACCE7DD8
5F7EF854 86B9743C FADC04AA FB0DA5C0
F913BE58 42FEA319 F954EFDD AE881E0B
------ END LICENSE ------
```
# 解决sublime text 3使用Install Package时出现There are no packages available for installation问题
网络的原因无法访问 https://packagecontrol.io/channel_v3.json 

所以我们自己指定一下channel_v3.json位置
[下载地址](https://share.weiyun.com/5g7cA6z)

打开`Preferences->Package Setting->Package Control ->Setting User`代码如下
{
    "bootstrapped": true,
    "channels":
    [
        "D:/channel_v3.json"
    ],
    "in_process_packages":
    [
    ],
    "installed_packages":
    [
        "ChineseLocalizations"
    ]
}




# 设置
```zsh
{
    "color_scheme": "Packages/Theme - Aprosopo/Tomorrow-Night-Eighties-Stormy.tmTheme",
    "font_face": "Consolas YaHei",
    "scroll_past_end": true,
    "font_size": 12,
    "margin": 5,
    "line_padding_top": 2, 
    "line_padding_bottom": 1, 
    "draw_centered": false,
    "ignored_packages":
    [
        "Vintage"
    ],
    "show_encoding": true,
    "show_line_endings": true,
    "theme": "Boxy Tomorrow.sublime-theme"
}

```
# php 常用插件
`SublimeLinter:` php代码检查

配置php引擎检查
```zsh
    "paths": {
        "linux": [],
        "osx": [],
        "windows": ["D:/phpstudy/PHPTutorial/php/php-7.0.12-nts"]
    },
```
`All Autocomplete：`

Sublime Text 默认的 Autocomplete 功能只考虑当前的文件，而 All Autocomplete 插件会搜索所有打开的文件来寻找匹配的提示词。

`SublimeTmpl:`

新建html、css、javascript、php、python、ruby六种类型的文件模板，所有的文件模板都在插件目录的templates文件夹里，可以自定义编辑文件模板。

```zsh
快捷键:
ctrl+alt+h html
ctrl+alt+j javascript
ctrl+alt+c css
ctrl+alt+p php
```
`SyncedSideBar：`

每次打开文件，侧边栏都会同步显示该文件所在目录树中的位置


`FileDiffs：`

强大的比较代码不同工具。比较当前文件与选中的代码、剪切板中代码、另一文件、未保存文件之间的差别。可配置为显示差别在外部比较工具，精确到行。右键标签页，出现FileDiffs
Menu或者Diff with Tab…选择对应文件比较即可

`BracketHighlighter` 高亮显示匹配的括号、引号和标签

`alignment :`自动对齐插件



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


# SFTP 
### 注册码
`SFTP-->setting user 填入下面这些`
```zsh
{  
    "email": "xiaosong@xiaosong.me",  
    "product_key": "d419f6-de89e9-0aae59-2acea1-07f92a"  
}  
 
// {  
// "email":"Rimke@163.com",  
// "product_key":"e83eda-38644b-43c828-e3669b-cd8a85",  
// }  
```
### 解决不能同步中文文件的问题 (windows下)
`网友的方法(已验证有效)`

<https://tieba.baidu.com/p/5496542324?red_tag=2962211545&traceid=>

`文件`

链接: <https://pan.baidu.com/s/130fSDkHxsIMZlPIJYANNoQ> 密码: qvc5

下载后,覆盖SFTP插件目录下的原版本(担心的可以备份一下原来的三个文件)

原因: 

经反编译后分析脚本代码后确认，

当服务端编码（Linux通常是utf-8）和本地编码（Windows通常是cp936）不一致时，

sftp的get和put命令及其应答结果中，包含的远端文件名和本地文件名也是不同编码的，

混合在一个字符串中，就会导致encode和decode报错。

对脚本进行了修正，分段进行encode和decode，就修复了此问题。

### SFTP 设置
```zsh
{
    // The tab key will cycle through the settings when first created
    // Visit http://wbond.net/sublime_packages/sftp/settings for help
    
    // sftp, ftp or ftps
    "type": "sftp",

    "save_before_upload": true, // 上传前保存在本地
    "upload_on_save": false,     // 保存时同时上传
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
----------------------------------------------------------------------------------- 