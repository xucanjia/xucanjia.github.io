---
layout: post
category: 技术
title: js方法处理富文本图片间隔问题
---
`js方法处理富文本图片间隔问题`
`自适应屏幕宽度`
```javascript
//富文本处理 
modifyRichText(description) {
	//修改富文本内容增加图片显示模式mode=widthFix
	var regex = new RegExp('<img', 'gi');
	description = description.replace(/\<img/gi, "< img style='width:100%;display:block;'");
	regex = new RegExp('<p', 'gi');
	description = description.replace(/\<p/gi, "<p style='width:100%;margin:0px;padding:0px;'");
	return description;
}
```