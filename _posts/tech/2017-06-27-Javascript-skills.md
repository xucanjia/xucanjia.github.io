---
layout: post
category: 技术
title: 重拾Javascript -_-!
---
## JavaScript用提示弹窗防止页面刷新和页面关闭误操作
Web开发中, 有时我们需要防止误操作引起的页面刷新和页面关闭, 

这个时候JavaScript可以帮到很大的忙, 

只需要在Ready中加入如下代码即可
```js
window.onbeforeunload = function(event){    
    return '您可能有数据没有保存!!!!'; 
};
```
当点击同意离开并使用相同窗口再次访问同一页面的时候，

本段JavaScript代码会失效(自动执行同意离开操作), 

建议每次都使用新窗口进行编辑操作
## JS输出空格
```javascript
document.write("&nbsp;&nbsp;&nbsp;"+"1"+"&nbsp;");// 傻办法

document.write("<span style='white-space: pre'>"+"1  2    3"+"</span>")
```
## jqury提示消息并自动消失
```zsh
Html:
<div id="successMsg" class="successMsg">

</div>
<style type="text/css">
.successMsg {
    width: 300px;
    display: none;
    color: #fff;
    text-align: center;
    position: fixed;
    top:20%;
    left: 40%;
    background: #3c763d;
    font-size: 16px;
    z-index: 9999;
    border:1px solid #ccc;
    border-radius: 5px;
    padding: 8px;
    align-content: center;
    box-shadow:2px 2px 5px #ddd;
}
</style>
js:
$("#successMsg").html("这里是消息！！！").show(300).delay(200).fadeOut(900);  

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
	var score; //score变量,用来存储用户输入的成绩值
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
`open()` 方法可以查找一个已经存在或者新建的浏览器窗口

`window.open([URL], [窗口名称], [参数字符串])`

参数说明:

URL:可选参数,在窗口中要显示网页的网址或路径 如果省略这个参数,或者它的值是空字符串,那么窗口就不显示任何文档

窗口名称:可选参数,被打开窗口的名称

    1.该名称由字母、数字和下划线字符组成

    2."_top"、"_blank"、"_self"具有特殊意义的名称

       _blank:在新窗口显示目标网页

       _self:在当前窗口显示目标网页

       _top:框架网页中在上部窗口中显示目标网页

    3.相同 name 的窗口只能创建一个,要想创建多个窗口则 name 不能相同

    4.name 不能包含有空格

参数字符串:可选参数,设置窗口参数,各参数用逗号隔开
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
文档对象模型DOM（Document Object Model）定义访问和处理HTML文档的标准方法

DOM 将HTML文档呈现为带有元素、属性和文本的树结构（节点树）

HTML文档可以说由节点构成的集合,三种常见的DOM节点:

1.`元素节点:` 上图中<html>、<body>、<p>等都是元素节点,即标签

2.`文本节点:` 向用户展示的内容,如<li>...</li>中的JavaScript、DOM、CSS等文本

3.`属性节点:` 元素属性,如a标签的链接属性href="http://www.imooc.com"

### 通过ID获取元素
`document.getElementById("id");`

### innerHTML 属性
`innerHTML` 属性用于`获取或替换 HTML 元素的内容`
注意:

1.Object是获取的`元素对象`,如通过document.getElementById("ID")获取的元素

2.注意书写,`innerHTML区分大小写`


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
// 如果要自定义初始值,可以用以下方法:
var d = new Date(2012, 10, 1);  //2012年10月1日
var d = new Date('Oct 1, 2012'); //2012年10月1日
```
![如](http://oi2atwmcz.bkt.clouddn.com/date.jpg)


## String 字符串对象
* `stringObject.length` 返回该字符串的长度

* `stringObject.toUpperCase()` 将字符串小写字母转换为大写

* `stringObject.toLowerCase()` 将字符串大写字母转换为小写

* `stringObject.charAt(index)` 返回指定位置的字符
	* 参数 index 不在 0 与 string.length-1 之间,该方法将返回一个`空字符串`,`一个空格也算一个字符`

* `stringObject.indexOf(substring, startpos)`
	* substring必须,要检索的字符,startpos 可选,不选从首字符开始
	* 返回 substring 的`第一次出现的位置`, 要检索的字符串值没有出现,则该方法返回 `-1`
	* indexOf() 方法区分大小写

* `stringObject.split(separator,limit)` 字符串分割
	* separator 必须,从该参数指定的地方分割
	* limit 可选,分割的次数,如设置该参数,`返回的子串不会多余这个参数指定的数组`,如果无此参数为不限制次数
	* 如果把空字符串 `("")` 用作 separator,那么 stringObject 中的每个字符之间都会被分割

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
	* 返回的内容是从 start开始(包含start位置的字符)到 stop-1 处的所有字符,其长度为 stop 减start
	* 如果参数 start 与 stop 相等,那么该方法返回的就是一个空串（即长度为 0 的字符串）
	* 如果 start 比 stop 大,那么该方法在提取子串之前会先交换这两个参数

* `stringObject.substr(startPos,length)` 提取指定数目的字符
	* startPos 必须,要提取字符串的起始位置,必须为数值,
	* 如果参数startPos是负数,从字符串的尾部开始算起的位置
	* 如果startPos为负数且绝对值大于字符串长度,startPos为0
	* length 可选 提取字符串的长度,若省略,提取startPos到字符对象的结尾


## Math 对象
Math 对象是一个`固有的对象`,无需创建它,

直接把 Math 作为对象使用就可以调用其所有属性和方法

* `Math.ceil(x)` 对一个数进行向上取整
	* 返回的是大于或等于x,并且与x最接近的整数

* `Math.floor(x)` 对一个数进行向下取整
	* 返回的是小于或等于x,并且与 x 最接近的整数

* `Math.round(x)` 把一个数字四舍五入为最接近的整数
	* 返回与 x 最接近的整数
	* 对于 0.5,该方法将进行上舍入 (5.5 将舍入为 6)
	* 如果 x 与两侧整数同等接近,则结果接近 +∞方向的数字值(如 -5.5 将舍入为 -5; -5.52 将舍入为 -6)

* `Math.random()` 随机数
	* 返回一个大于或等于 0 但小于 1 的符号为正的数字值

# Array 数组对象

* 定义了一个空数组:
	* `var  数组名= new Array();`
* 定义时指定有n个空元素的数组:
	* `var 数组名 =new Array(n);`
* 定义数组的时候,直接初始化数据:
	* `var  数组名 = [<元素1>, <元素2>, <元素3>...];`

![](http://oi2atwmcz.bkt.clouddn.com/array.jpg)

* `arrayObject.join(分隔符)` 指定分隔符连接数组元素
* `arrayObject.reverse()` 颠倒数组中元素的顺序
* `arrayObject.slice(start,end)` 从已有的数组中返回选定的元素
* `arrayObject.sort(方法函数)` 使数组中的元素按照一定的顺序排列
	* 如果不指定<方法函数>,则按unicode码顺序排列
	* 如果指定<方法函数>,则按<方法函数>所指定的排序方法排序


# window 对象

`window对象是BOM的核心,window对象指当前的浏览器窗口`

![](http://oi2atwmcz.bkt.clouddn.com/bom.jpg)

* 计时器
	* `setTimeout()` 指定的延迟时间之后执行代码
		* `setTimeout(函数/代码,延迟时间)`
	* `clearTimeout()` 取消setTimeout()设置
		* `clearTimeout(id_of_setTimeout)` id_of_setTimeout: 由 setTimeout() 返回的 ID 值

	* `setInterval()` 每隔指定的时间执行代码
		* `setInterval(函数/代码,交互时间)` 以毫秒计（1s=1000ms）
	* `clearInterval()` 取消setInterval()设置
		* clearInterval(id_of_setInterval) id_of_setInterval: 由 setInterval() 返回的 ID 值

# History 对象

history对象记录了用户曾经浏览过的页面(URL),并可以实现浏览器前进与后退相似导航的功能

* window.history.[属性|方法]
	* History `对象属性`:
		* 如 var HL = window.history.length;
	* History `对象方法`:
		* `back()` 加载history列表中的前一个URL
			* 如 window.history.back();
		* `forward()` 加载history列表中的下一个URL
			* window.history.forward();
		* `go()` 加载history列表中的某个具体的页面
			* window.history.go(-1);

# Location对象

location用于获取或设置窗体的URL,并且可以用于解析URL

![](http://oi2atwmcz.bkt.clouddn.com/location.jpg)

* location.(属性/方法)
	* location 对象属性:

	![对象属性](http://oi2atwmcz.bkt.clouddn.com/location%E5%AF%B9%E8%B1%A1%E5%B1%9E%E6%80%A7.jpg)

	* location 对象方法:

	![对象方法](http://oi2atwmcz.bkt.clouddn.com/location%E5%AF%B9%E8%B1%A1%E6%96%B9%E6%B3%95.jpg)


# Navigator对象
Navigator 对象包含有关浏览器的信息,通常用于检测浏览器与操作系统的版本

* 对象属性:

![](http://oi2atwmcz.bkt.clouddn.com/navigator.jpg)

* navigator.userAgent 返回用户代理头的字符串表示(就是包括浏览器版本信息等的字符串)

![](http://oi2atwmcz.bkt.clouddn.com/useragent.jpg)

# screen对象
* `window.screen.属性` 获取用户的屏幕信息

![](http://oi2atwmcz.bkt.clouddn.com/screen.jpg)

* screen.height 返回屏幕分辨率的高
* screen.width 返回屏幕分辨率的宽
注:单位以像素计window.screen 对象在编写时可以不使用 window 这个前缀


* 屏幕可用高和宽度
	* screen.availWidth 属性返回访问者屏幕的宽度,以像素计,减去界面特性,比如任务栏

	* screen.availHeight 属性返回访问者屏幕的高度,以像素计,减去界面特性,比如任务栏


# DOM

DOM节点层次图

![](http://oi2atwmcz.bkt.clouddn.com/domjiedian.jpg)

### DOM节点有:

1. `元素节点:` 上图中<html>、<body>、<p>等都是元素节点,即标签

2. `文本节点:` 向用户展示的内容,如<li>...</li>中的JavaScript、DOM、CSS等文本

3. `属性节点:` 元素属性,如a标签的链接属性href="http://www.imooc.com"


* `节点属性`

| 方法           | 说明           |
| ------------- |:-------------:|
| nodeName      | 返回一个字符串,其内容是给定节点的名字  |
| nodeType      | 返回一个整数,这个数值代表给定节点的类型 |
| nodeValue     | 返回给定节点的当前值                |

* `遍历节点树`

| 方法           | 说明           |
| ------------- |:-------------:|
| childNodes      | 返回一个数组,这个数组由给定元素节点的子节点构成  |
| fistChild       | 返回第一个子节点						    |
| lastChild       | 返回最后一个子节点       					|
| parentNode      | 返回一个给定节点的父节点              	    |
| nextSibling     | 返回给定节点的下一个子节点                	|
| previousSibling | 返回给定节点的上一个子节点                	|


### DOM操作:

文档对象模型DOM 定义访问和处理HTML文档的标准方法 DOM 将HTML文档呈现为带有元素、属性和文本的树结构（节点树）


| 方法           | 说明           |
| ------------- |:-------------:|
| createElement(element)      | 创建一个新的元素节点  |
| createTextNode()       | 创建一个包含着给定文本的新文本节点 |
| appendChild()       | 返回最后一个子节点列表之后添加一个新的子节点 |
| insertBefore()      | 将一个给定节点插入到一个给定元素节点的给定子节点的前面 |
| removeChild()     | 从一个给定元素中删除一个子节点 |
| replaceChild() | 把一个给定父元素里的一个子节点替换为另外一个节点 |


1. `document.getElementById(id)` 通过指定id获得元素(获得一个)

2. `document.getElementsByName(name)` 返回带有指定名称的节点对象的集合

3. `document.getElementsByTagName(Tagname)` 返回带有指定标签名的节点对象的集合 返回元素的顺序是它们在文档中的顺序

4. `elementNode.getAttribute(name)` 通过元素节点的属性名称获取属性的值
	* elementNode: 使用getElementById()、getElementsByTagName()等方法,获取到的元素节点
	* name: 要想查询的元素节点的属性名字

5. `elementNode.setAttribute(name,value)` 增加一个指定名称和值的新属性,或者把一个现有的属性设定为指定的值
	* name: 要设置的属性名
	* value: 要设置的属性值


### 节点属性
在文档对象模型 (DOM) 中, 每个节点都是一个对象 DOM 节点有三个重要的属性:

* nodeName:节点的名称,是只读的
	* 元素节点的 nodeName 与标签名相同
	* 属性节点的 nodeName 是属性的名称
	* 文本节点的 nodeName 永远是 #text
	* 文档节点的 nodeName 永远是 #document

* nodeValue:节点的值
	* 元素节点的 nodeValue 是 undefined 或 null
	* 文本节点的 nodeValue 是文本自身
	* 属性节点的 nodeValue 是属性的值

* nodeType:节点的类型

| 元素类型         | 节点类型         |
| ------------- |:-------------:|
| 元素      | 1  |
| 属性       | 2 |
| 文本       | 3|
| 注释      | 8|
| 文档     | 9 |

```javascript
var node=document.getElementsByTagName("li");
for(var i=0;i<node.length;i++){
    document.write("节点名称"+ node[i].nodeName+"<br>");
    document.write("节点的值"+node[i].nodeValue+"<br>");
    document.write("节点的类型"+node[i].nodeType+"<br>");
}
```
* `elementNode.childNodes` 访问选定元素节点下的所有子节点的列表, 返回的值可以看作是一个数组,具有length属性

如果选定的节点没有子节点, 则该属性返回不包含节点的 NodeList


* 访问子节点的第一和最后项
	* node.firstChild 属性返回‘childNodes’数组的第一个子节点, 如果选定的节点没有子节点, 则该属性返回 NULL 与elementNode.childNodes[0]是同样的效果
	* node.lastChild 与elementNode.childNodes[elementNode.childNodes.length-1]是同样的效果

* nodeObject.nextSibling 返回某个节点之后紧跟的节点（处于同一树层级中）如果无此节点, 则该属性返回 null

* nodeObject.previousSibling 可返回某个节点之前紧跟的节点（处于同一树层级中）如果无此节点, 则该属性返回 null


* appendChild(newnode) 在指定节点的最后一个子节点列表之后添加一个新的子节点

* insertBefore(newnode,node) newnode:要插入的新节点 node: 指定此节点前插入节点

* nodeObject.removeChild(node) 从子节点列表中删除某个节点.如删除成功, 此方法可返回被删除的节点, 如失败, 则返回 NULL.

* node.replaceChild (newnode,oldnew ) 实现子节点(对象)的替换.返回被替换对象的引用

* document.createElement(tagName) 创建元素节点.此方法可返回一个 Element 对象

* document.createTextNode(data) 创建新的文本节点, 返回新创建的 Text 节点

### 浏览器窗口可视区域大小
获得浏览器窗口的尺寸（浏览器的视口, 不包括工具栏和滚动条）的方法:

1. 对于IE9+、Chrome、Firefox、Opera 以及 Safari:

* `window.innerHeight` - 浏览器窗口的内部高度
* `window.innerWidth` - 浏览器窗口的内部宽度

2. 对于 Internet Explorer 8、7、6、5:

* `document.documentElement.clientHeight` 表示HTML文档所在窗口的当前高度.
* `document.documentElement.clientWidth` 表示HTML文档所在窗口的当前宽度.

或者

Document对象的body属性对应HTML文档的<body>标签

* `document.body.clientHeight`
* `document.body.clientWidth`

在不同浏览器都实用的 JavaScript 方案:
```javascript
var w= document.documentElement.clientWidth
      || document.body.clientWidth;
var h= document.documentElement.clientHeight
      || document.body.clientHeight;
```

### 网页尺寸scrollHeight
`scrollHeight` 和 `scrollWidth`, 获取网页内容高度和宽度.

1. 针对IE、Opera:

`scrollHeight` 是`网页内容实际高度`, 可以小于 clientHeight.

2. 针对NS、FF:

`scrollHeight` 是`网页内容高度`, 不过最小值是 clientHeight 也就是说网页内容实际高度小于 clientHeight 时, scrollHeight 返回 clientHeight.

3. 浏览器兼容性
```javascript
var w=document.documentElement.scrollWidth
   || document.body.scrollWidth;
var h=document.documentElement.scrollHeight
   || document.body.scrollHeight;
// 注意:区分大小写
```
`scrollHeight和scrollWidth还可获取Dom元素中内容实际占用的高度和宽度.`


### 网页尺寸offsetHeight
`offsetHeight` 和`offsetWidth`, 获取网页内容高度和宽度(包括滚动条等边线,会随窗口的显示大小改变)。

1. 值

`offsetHeight = clientHeight + 滚动条 + 边框`

2. 浏览器兼容性
```javascript
var w= document.documentElement.offsetWidth
    || document.body.offsetWidth;
var h= document.documentElement.offsetHeight
    || document.body.offsetHeight;
```

###网页卷去的距离与偏移量

i[](http://oi2atwmcz.bkt.clouddn.com/offset.jpg);

`scrollLeft`: 设置或获取位于给定对象左边界与窗口中目前可见内容的最左端之间的距离, 即左边灰色的内容。

`scrollTop`: 设置或获取位于对象最顶端与窗口中可见内容的最顶端之间的距离, 即上边灰色的内容。

`offsetLeft`: 获取指定对象相对于版面或由 offsetParent 属性指定的父坐标的计算左侧位置 。

`offsetTop`: 获取指定对象相对于版面或由 offsetParent 属性指定的父坐标的计算顶端位置 。

注意:

	* 区分大小写
	* offsetParent：布局中设置postion属性(Relative、Absolute、fixed)的父容器，从最近的父节点开始，一层层向上找，直到HTML的body。


参考:慕课网
