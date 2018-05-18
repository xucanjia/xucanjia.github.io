---
layout: post
category: ['mysql']
title: mysql相关
---
#关于批量更新
### 批量修改某个字段,根据某个条件
```zsh
UPDATE categories 
    SET display_order = CASE id 
        WHEN 1 THEN 3 
        WHEN 2 THEN 4 
        WHEN 3 THEN 5 
    END
WHERE id IN (1,2,3)
```
更新 `display_order` 字段，

`如果id=1 则display_order 的值为3，如果id=2 则 display_order 的值为4...`
即是将条件语句写在了一起。

这里的where部分不影响代码的执行，

但是会提高sql执行的效率。

确保sql语句仅执行需要修改的行数，

这里只有3条数据进行更新，

而where子句确保只有3行数据执行。

### 更新多个值的话，只需要稍加修改：
```zsh
UPDATE categories 
    SET display_order = CASE id 
        WHEN 1 THEN 3 
        WHEN 2 THEN 4 
        WHEN 3 THEN 5 
    END, 
    title = CASE id 
        WHEN 1 THEN 'New Title 1'
        WHEN 2 THEN 'New Title 2'
        WHEN 3 THEN 'New Title 3'
    END
WHERE id IN (1,2,3)
```

### 当使用上万条记录利用mysql批量更新，发现使用最原始的批量update发现性能很差

`网上最优方法`

`另外三种批量更新方式`

1. replace into 批量更新

```zsh
replace into mytable(id, myfield) values (1,'value1'),(2,'value2'),(3,'value3');
```

2. insert into ...on duplicate key update批量更新

```zsh
insert into mytable(id, myfield1, myfield2) values (1,'value11','value21'),(2,'value12','value22'),(3,'value13','value23') on duplicate key update myfield1=values(myfield2),values(myfield2)+values(id);
```
3. 临时表
```zsh
DROP TABLE IF EXISTS `tmptable`;
create temporary table tmptable(id int(4) primary key,myfield varchar(50));
insert into tmptable values (1,'value1'),(2,'value2'),(3,'value3');
update mytable, tmptable set mytable.myfield = tmptable.myfield where mytable.i
```

【replace into】和【insert into】更新都依赖于`主键`或`唯一值`，并都可能造成`新增记录`的操作的结构隐患

【replace into】操作本质是`对重复记录先delete然后insert`，`如果更新的字段不全缺失的字段将被设置成缺省值`

【insert into】则只是update重复的记录，更改的字段只能依循公式值

【临时表】方式需要用户有temporary 表的create 权限

 `数量较少时【replace into】和【insert into】性能最好，数量大时【临时表】最好, 【CASE】则具有通用型也不具结构隐患`
 
 ------