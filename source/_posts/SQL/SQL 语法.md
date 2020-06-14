---
title: SQL语法
translate_title: SQL语法
comments: false
date: 2016-09-25 12:13:00
categories:
  - SQL
tags:
  - SQL
  - MySQL
---
SQL 语法
==========
### 日期获取 ###
- 获取当前日期时间
```sql
select now();
select sysdate();
```
- 获取当前日期
```sql
select curdate();
select current_date;
```
- 获取当前时间 hh:mi:ss
```sql
select time(sysdate());
```
- 获取 年、月、日、时、分、秒、毫秒
```sql
/*年*/
select year(current_date);
/*月*/
select month(current_date);
/*日*/
select day(current_date);
/*时*/
select hour(sysdate());
/*分*/
select minute(sysdate());
/*秒*/
select second(sysdate());
/*毫秒*/
select microsecond(sysdate());
```
### 日期函数 ###
- 日期运算
```sql
/*带时分秒的源日期计算之后也带时分秒*/
/*前一年*/
select date_sub(curdate(), interval 1 year);
/*前一月*/
select date_sub(curdate(), interval 1 month);
/*前一天日期*/
select date_sub(curdate(), interval 1 day);
/*前一小时*/
select date_sub(sysdate(), interval 1 hour);
/*前一分*/
select date_sub(sysdate(), interval 1 minute);
/*前一秒*/
select date_sub(sysdate(), interval 1 second);
```
### 日期格式化 ###
```sql
/*yyyy-mm-dd hh24:mi:ss*/
select str_to_date('2016-09-23 16:03:28', '%Y-%m-%d %H:%i:%s');
/*yyyy-mm-dd*/
select str_to_date('2016-09-23 16:03:28', '%Y-%m-%d');
```
### if 函数 ###
- if
```sql
select if('0' = '1', 0, 1);
select if(0 != 1, 0, 1);
```
- ifnull
```sql
select ifnull(null, 0);
select ifnull(1, 0);
```
