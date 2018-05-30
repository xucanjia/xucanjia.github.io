---
layout: post
category: ['Thinkphp5']
title: Thinkphp5 基础
---
# 配置
todo~~~
---------------
# 路由
需要在配置文件 `根目录/conf/config.php中` `开启路由`（默认是开启）
```php
url_route_ont => true, // 开启路由
url_route_must => false,// 强制路由 开启后必须使用路由访问
```
```php
// 控制器中 默认这样
localhost/index/index/info/id/5
public function info($id)
{
	echo "{$id}";	
}

```
`如果想直接访问 localhost/info 需要在配置文件 根目录/conf/route.php`
```php
return [
	'info/:id' => 'index/index/info',
];
```
`同样的url()函数也会随之得到路由后的地址`
--------------