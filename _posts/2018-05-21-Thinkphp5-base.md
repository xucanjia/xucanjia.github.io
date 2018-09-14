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

# setField 更新某字段的值
```php
$User = M("User"); // 实例化User对象
// 更改用户的name值
$User-> where('id=5')->setField('name','ThinkPHP');

//setField方法支持同时更新多个字段，只需要传入数组即可，例如：
$User = M("User"); // 实例化User对象
// 更改用户的name和email的值
$data = array('name'=>'ThinkPHP','email'=>'ThinkPHP@gmail.com');
$User-> where('id=5')->setField($data);
// 而对于统计字段（通常指的是数字类型）的更新，系统还提供了setInc和setDec方法。
$User = M("User"); // 实例化User对象
$User->where('id=5')->setInc('score',3); // 用户的积分加3
$User->where('id=5')->setInc('score'); // 用户的积分加1
$User->where('id=5')->setDec('score',5); // 用户的积分减5
$User->where('id=5')->setDec('score'); // 用户的积分减1
// 延迟更新
// setInc/setDec支持延时更新，如果需要延时更新则传入第三个参数
// 下例中延时10秒，给score字段增加1
Db::table('think_user')->where('id', 1)->setInc('score', 1, 10);
```
# 更新数据表中的数据
```php
Db::table('think_user')->where('id', 1)->update(['name' => 'thinkphp']);
//如果数据中包含主键，可以直接使用：
Db::table('think_user')->update(['name' => 'thinkphp','id'=>1]);
// 更新的数据需要使用SQL函数或者其它字段
Db::table('think_user')
    ->where('id', 1)
    ->update([
        'login_time'  => ['exp','now()'],
        'login_times' => ['exp','login_times+1'],
    ]);
```