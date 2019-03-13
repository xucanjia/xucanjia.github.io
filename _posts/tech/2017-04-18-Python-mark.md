---
layout: post
category: 技术
title: Python3 笔记
---
member = [1,2,3,4]
# 列表
## 向列表添加元素
append('gg') 列表末尾添加
extend(['jj', '76']) 列表末尾添加 参数用一个列表添加到一个列表
insert(1,['kjkj'])指定位置插入元素

## 列表删除元素
remove('kjkj')
del member[1]
member.pop() 删除最后一元素 返回 删除元素的值
member.pop(2) 删除指定元素 返回 删除元素的值

## 切片
member[1:3] 从下标1开始 返回三个元素
member[:3] 从下标0开始 返回三个元素
member[:] 原列表的拷贝

# 元组
temp = (1,2,3,4)
temp = 1,2,3
识别元组的关键是 逗号  ,  不是括号
 ## 更新和删除元组
 用切片的放方式
 ## 元组操作符
