---
layout: post
category: ['Thinkphp']
title: Thinkphp搜索+分页的问题
---
## 搜索+分页的问题
最近在做后台数据集的整理,

涉及到了多条件搜索带分页展示,

其实,

我是先做好了分页,后面才去做多条件搜索的.先贴一段小代码.

```html
<!--search start-->
<form class="searchform" action="__URL__/index" method="POST">
    <input type="text" class="form-control" name="k" placeholder="Search here..." />
    <input type="submit" name="搜索">
</form>
<!--search end-->
```
不知道找到了问题没有?

**提示**
`进行分页数据查询 注意page方法的参数的前面部分是当前的页数使用 $_GET[p] 获取`

**问题在于** `POST`

**搜索分页时候表单提交用的是**`GET`方式

当然,假如我们要用POST提交呢

可以去参考这篇文章,

-<http://blog.csdn.net/arzhuo/article/details/6969516>

`凡事要细心,祭奠死去的时间....`
