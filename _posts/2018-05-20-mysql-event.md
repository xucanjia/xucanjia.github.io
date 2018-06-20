---
layout: post
category: ['mysql']
title: mysql定时执行脚本
---
## 查看定时
```zsh
SHOW EVENTS  

select * from mysql.event
```

## 设置定时
```zsh
# 登陆
mysql -u root -p  

# 查看是否开启event
show variables like '%sche%';

# 开启event (防止计划任务重启后消失)
set global event_scheduler=1;

# 创建存储过程
CREATE PROCEDURE test ()   
BEGIN   
UPDATE bll_productkill SET STATUS=0 WHERE ed_time<NOW();  
END;  

# 创建event e_test
create event if not exists e_test   
on schedule every 30 second   
on completion preserve   
do call test();  

# 关闭事件任务
alter event e_test ON COMPLETION PRESERVE DISABLE;  

# 每天定时执行任务，设置第一次执行时间为'2017-06-18 01:00:00'，并且每天执行一次  
create event if not exists e_test   
on shcedule every 1 day starts '2017-06-18 01:00:00'  
do call test();   
```

`如用数据库可视化工具,如Navicate,可直接建立定时任务方便快捷`
