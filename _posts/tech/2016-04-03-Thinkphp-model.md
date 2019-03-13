---
layout: post
category: 技术
title: Thinkphp模型的理解
---

### 1、创建一个基础模型：实例化一个系统自带的数据库操作类

`Test.Model.class.php`
```php
class TestModel extends Model
{
  // ...
}
```
`UserAction.class.php`
```php
function test()
{
  //表示实例化的是自带的Model类，并且传入test值表示操作的是test表
  $test=M('test');
  //等同于$test=new TestModel();
  $test=$test->select();
  print_r($test);//输出test表中所有数据
}
```
### 2、实例化一个自定义模型

如果数据库操作比较复杂，就需要在自定义的Model类中添加一些自定义的数据库操作方法

`UserModel.class.php`
```php
class UserModel extends Model
{
  function pyj()
  {
    echo 'penyanjie';
    //其它的一些数据库操作方法
  }
}
```
`UserAction.class.php`
```php
function user()
{
  $user=D('User');//实例化自定义的数据库操作类
  //等同于$user=new UserModel();
  $user->pyj();//调用User模型中的pyj方法
}
```
或者，你需要实例化一个表，

同时呢，实例化一个自己写的自定义的数据库操作类，
```php
function love()
{
  $love=M('test','UserModel');
  //$love=new UserModel('test');
  $list=$love->select();
  dump($list);
  $love->pyj();
}
```
### 3、实例化一个用户模型

`UserAction.class.php`

```php
function user()
{
  $user=new UserModel();//等同于$user=D('User');
  $list=$user->select();
  dump($list);
  echo $user->aa();
}
```
`UserModel.class.php`

该类名user与表名user相对应，

所以在UserAction中实例化这个模型的时候就不需要再额外的传表名了
```php
class UserModel extends Model
{
  function aa()
  {
    echo 'pengyanjie';
  }
}
```

`这个第三种实例化模型方法与第二种的区别在于：`

`在你的业务逻辑当中，`

`通常情况下会有一些公共的业务逻辑，`

`那你用第二种M('表名','模型名');`

`如M('user','CommonModel')会更方便;`

`第三种实例化模型方法适于于针对所操作表的更加复杂的业务逻辑，`

`但是它不需要使用到公共业务逻辑。`

`（它的业务逻辑，针对用户表，它是唯一的，并且不需要在其它模型当中使用）。`

### 4、实例化一个空模型，

它并不知道你要实例化操作时用到的是哪张表。

```php
$user=new Model();//等价与$user=M();

$list=$user->query('select * from think_user');

//使用传统的sql语句的方式，如果这样的话，就必须要加表前缀
dump($list);
```
### 附：
`$user=new UserModel();与$user=D('user')` **的区别:**

`D方法可以自动检测模型类，不存在时，它会抛出一个异常。同时对于已实例化过的模型，不会去重复实例化。默认的D方法，只能应用于当前项目下面的模型。`

`如果说，我这是前台应用，但是我想实例化后台项目的模型可以用D搞定`

```php
$user=D('admin','user');//会去自动找admin分组下的user模型类
```
`或者:`
```php
$user=D('admin.user');
```
