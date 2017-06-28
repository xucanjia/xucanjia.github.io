---
layout: post
category: ['Javascript']
title: 重拾Javascript -_-!
---
## JS输出空格
```javascript
document.write("&nbsp;&nbsp;&nbsp;"+"1"+"&nbsp;");// 傻办法

document.write("<span style='white-space: pre'>"+"1  2    3"+"</span>")
```

## confirm 消息确认对话框
返回值:

当用户点击 `"确定"` 按钮时,返回 `true`

当用户点击 `"取消"` 按钮时,返回 `false`
```javascript
function rec(){
	var mymessage=confirm("你喜欢js吗?"); // 这样也行 -_-!
	if(mymessage==true)
	{
		document.write("000");
	}
	else
	{
	    document.write("111");
	}
}
```
## 提问 prompt 消息对话框
`prompt(str1, str2);`

`str1:`要显示在消息对话框中的文本,不可修改

`str2:`文本框中的内容,可以修改

返回值:

1.点击确定按钮,`文本框中的内容将作为函数返回值`

2.点击取消按钮,将返回 `null`
```javascript
function rec(){
	var score; //score变量,用来存储用户输入的成绩值。
	score =prompt("请输入你的成绩",score);
	if(score>=90)
	{
	   document.write("你很棒!");
	}
	else if(score>=75)
	{
	   document.write("不错吆!");
	}
	else if(score>=60)
	{
	   document.write("要加油!");
	}
	else
	{
	   document.write("要努力了!");
	}
}
```
## 打开新窗口 window.open
`open()` 方法可以查找一个已经存在或者新建的浏览器窗口。

`window.open([URL], [窗口名称], [参数字符串])`

参数说明:

URL:可选参数,在窗口中要显示网页的网址或路径。如果省略这个参数,或者它的值是空字符串,那么窗口就不显示任何文档。

窗口名称:可选参数,被打开窗口的名称。

    1.该名称由字母、数字和下划线字符组成。

    2."_top"、"_blank"、"_self"具有特殊意义的名称。

       _blank:在新窗口显示目标网页

       _self:在当前窗口显示目标网页

       _top:框架网页中在上部窗口中显示目标网页

    3.相同 name 的窗口只能创建一个,要想创建多个窗口则 name 不能相同。

    4.name 不能包含有空格。

参数字符串:可选参数,设置窗口参数,各参数用逗号隔开。
```javascript
window.open("http://www.baidu.com","_blank","width=600,height=400,top=100,left=0");
```

## 关闭窗口 window.close

`close()关闭窗口`

`window.close();` 关闭本窗口

或

`<窗口对象>.close();` 关闭指定的窗口


```javascript
var win=window.open("http://www.baidu.com");
setTimeout("winClose()",5000);
function winClose(){
	win.close(win);
}
```


# 认识 DOM
文档对象模型DOM（Document Object Model）定义访问和处理HTML文档的标准方法。

DOM 将HTML文档呈现为带有元素、属性和文本的树结构（节点树）。

HTML文档可以说由节点构成的集合,三种常见的DOM节点:

1.`元素节点:` 上图中<html>、<body>、<p>等都是元素节点,即标签。

2.`文本节点:` 向用户展示的内容,如<li>...</li>中的JavaScript、DOM、CSS等文本。

3.`属性节点:` 元素属性,如<a>标签的链接属性href="http://www.imooc.com"。

### 通过ID获取元素
`document.getElementById("id");`

### innerHTML 属性
`innerHTML` 属性用于`获取或替换 HTML 元素的内容`。
注意:

1.Object是获取的`元素对象`,如通过document.getElementById("ID")获取的元素。

2.注意书写,`innerHTML区分大小写`。


### 改变 HTML 样式
语法:

`Object.style.property=new style;`

```javascript
var mychar= document.getElementById("con");
mychar.style.color="red";
mychar.style.backgroundColor="#CCC";
mychar.style.width="300px";
```
## 显示和隐藏（display属性）
`Object.style.display = value;`
value:

`none`  此元素将被隐藏

`block` 此元素将被显示

## 控制类名（className 属性）
`object.className = classname;`

# 事件
`onfocus 光标聚焦事件`

`onblur 失焦事件`

`onselect 选中事件`

`onchange 文本框内容改变事件`

`onload 加载事件` 写在<body>标签内


# 对象

## Date 日期对象
```javascript
var Udate=new Date();
// 如果要自定义初始值，可以用以下方法：
var d = new Date(2012, 10, 1);  //2012年10月1日
var d = new Date('Oct 1, 2012'); //2012年10月1日
```
![如](http://oi2atwmcz.bkt.clouddn.com/date.jpg)


## String 字符串对象
* `stringObject.length` 返回该字符串的长度

* `stringObject.toUpperCase()` 将字符串小写字母转换为大写

* `stringObject.toLowerCase()` 将字符串大写字母转换为小写

* `stringObject.charAt(index)` 返回指定位置的字符
	* 参数 index 不在 0 与 string.length-1 之间，该方法将返回一个`空字符串`,`一个空格也算一个字符`

* `stringObject.indexOf(substring, startpos)`
	* substring必须,要检索的字符,startpos 可选,不选从首字符开始
	* 返回 substring 的`第一次出现的位置`, 要检索的字符串值没有出现，则该方法返回 `-1`
	* indexOf() 方法区分大小写

* `stringObject.split(separator,limit)` 字符串分割
	* separator 必须,从该参数指定的地方分割
	* limit 可选,分割的次数,如设置该参数,`返回的子串不会多余这个参数指定的数组`,如果无此参数为不限制次数
	* 如果把空字符串 `("")` 用作 separator，那么 stringObject 中的每个字符之间都会被分割。

```javascript
var mystr = "www.xucanjia.com";
document.write(mystr.split(".", 2)+"<br>");
// www,xucanjia

document.write(mystr.split("", 5));
// w,w,w,.,x
```
* `stringObject.substring(startPos,stopPos) ` 提取字符串
	* startPos 必须,一个非负的整数,开始位置
	* stopPos 可选,一个非负整数,结束位置,若省略,返回的子串会到对象结尾
	* 返回的内容是从 start开始(包含start位置的字符)到 stop-1 处的所有字符，其长度为 stop 减start
	* 如果参数 start 与 stop 相等，那么该方法返回的就是一个空串（即长度为 0 的字符串）
	* 如果 start 比 stop 大，那么该方法在提取子串之前会先交换这两个参数
