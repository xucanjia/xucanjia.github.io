---
layout: post
category: ['Thinkphp']
title: Thinkphp的坑
---

## 输出模板和作判断的坑的


`模板中已注释的代码`
```html
<!-- <if condition="{$Think.CONTROLLER_NAME} eq 'Order'">active
<else /> other Framework
</if> -->
```
虽然此段`代码写错了`,但是由于我`已经注释`,结果还是`报语法错误~`

`syntax error, unexpected '{'`

一开始并没注意代码写错,况且也已经注释,不应该报错.

最后我去查看缓存html文件,才发现代码错,

忙着改成下面的,
```html
<eq name="Think.CONTROLLER_NAME" value="Order" >avtive</eq>
```


### 完整的判断
```html
 <li class="menu-list <eq name='Think.CONTROLLER_NAME' value='Order' >active</eq> ">
 </li>
```


`总结: 模板输出的时候,代码写错,就算注释了,Tp框架也会报错~.~!`
