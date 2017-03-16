---
layout: post
category: ['PHP']
title: PHP的闭包（Closure) 匿名函数
---

 `php中的 匿名函数(Anonymous functions), 也叫 闭包函数(closures)`

 `允许指定一个没有名称的函数, 最常用的就是回调函数的参数值`


## 匿名函数:
```php
$closureFunc = function(){
　　　// code...
};
```
### eg:
```php
$closureFunc = function($str){
　　 echo $str;
  };
$closureFunc("hello world!");
```
**输出** `hello world!`

## 闭包:
### 1.将匿名函数放在普通函数中，也可以将匿名函数返回，这就构成了一个简单的闭包
```php
function closureFunc1(){
    $func = function(){
        echo "hello";
    };
    $func();
}
closureFunc1();
```
**输出** `hello`

### 2.在匿名函数中引用局部变量

我们不能在匿名函数中直接使用`局部变量`，

这时候就要引用一个php的关键字 `use`，
```php
function closureFunc2(){
    $num = 1;
    $func = function() use($num){
        echo $num;
    };
    $func();
}
closureFunc2();
```
**输出** `1`

### 3.返回匿名函数(也可传参)
```php
function closureFunc3(){
    $num = 1;
    $func = function($str) use($num){
        echo $num;
        echo "\n";
        echo $str;
    };
    return $func;
}
$func = closureFunc3(); //函数返回匿名函数
$func("hello"); //然后我们在用$func() 调用 传参也是如此
```
**输出** `1`

**输出** `hello`

`若想用闭包来改变上下文引用的变量值`

如改变 **$num** , 只需在这样写 `&$num`.

### 4.把匿名函数当作参数传递
```php
function callFunc($func){
    $func("111");
}

callFunc(function($str){
    echo $str;
})
```
**输出** `111`
