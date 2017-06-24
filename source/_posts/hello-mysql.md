---
title: MySql 命令
date: 2017-06-18
tags: mysql
---

##### 登录MySQL
    mysql -h192.168.0.1 -uroot -proot
<!-- more -->
##### 退出MySQL
    exit || quit
##### 创建数据库
    create database test_db
##### 显示所有数据库
    show databases
##### 选择数据库
    use test_db
##### 创建表
    create table test
    (id int unsigned not null auto_increment primary key, 
    name varchar not null)
##### 向表中插入数据
    insert [into] 表名 [(列名1, 列名2, 列名3, ...)] values (值1, 值2, 值3, ...);
##### 查询表中的数据
    select 列名称 from 表名称 [查询条件];
##### 更新表中的数据
    update 表名称 set 列名称=新值 where 更新条件;
##### 删除表中的数据
    delete from 表名称 where 删除条件;
#### 创建后对表的修改
##### 添加列
    alter table 表名 add 列名 列数据类型 [after 插入位置];
##### 修改列
    alter table 表名 change 列名称 列新名称 新数据类型;
##### 删除列
    alter table 表名 drop 列名称;
##### 重命名表
    alter table 表名 rename 新表名;
##### 删除表
    drop table 表名;
##### 删除数据库
    drop database 数据库名;
##### 修改 root 用户密码
    mysqladmin -u root -p password 新密码