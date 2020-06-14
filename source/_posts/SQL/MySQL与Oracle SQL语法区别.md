---
title: MySQL与Oracle SQL语法区别
translate_title: MySQL与Oracle SQL语法区别
comments: false
date: 2016-09-23 18:16:00
categories:
  - SQL
tags:
  - SQL
  - MySQL
  - Oracle
---
MySQL与Oracle SQL语法区别
==========
> 最近因为客户公司主张 `去IOE`，所以要求把项目上使用的 `Oracle` 数据库切换到 `MySQL`，所以花了点时间对项目进行重构，主要工作是修改 `SQL` 语法上，总结下重构过程遇到的 Oracle 和 MySQL 的语法区别，因为采用了 `MyBatis` 作为 ORM 框架，所以顺便把两种数据库都做了支持，配置切换。
# 日期类
- MySQL
```sql
-- 获取当前日期
select curdate();
select current_date;
-- 获取当前时间
select now();
select sysdate();
-- 获取时间中的年月日部分
select date(now());
-- 获取时间中的时分秒部分
select time(now());
```
- Oracle
```sql
-- 获取当前时间
select sysdate from dual;
```
# 日期字符串转换 
- MySQL
```sql
/* 字符串转为时间格式 */
select str_to_date('2016-09-23 16:03:30', '%Y-%m-%d %H:%i:%s');
-- 2016-09-23 16:03:30
select str_to_date('2016-09-22 16:03:30', '%Y-%m-%d');
-- 2016-09-22
```
- Oracle
```sql
/* 字符串转为时间格式，分秒不会消失 */
select to_date('2016-09-23 16:03:30', 'yyyy-mm-dd hh24:mi:ss') from dual;
-- 2016-09-23 16:03:30
select to_date('2016-09-22', 'yyyy-mm-dd') from dual;
-- 2016-09-22 00:00:00
```
# 简单判断函数 
- MySQL if函数
```sql
/* if(exp,attr0,attr1),如果exp为true，则返回attr0，false则返回attr1*/
select if('0'='1',0,1);
-- 1
select if(0!=1,0,1);
-- 0
```
- Oracle decode
```sql
/* decode(exp0,exp1,attr0,attr1),如果exp0=exp1,则返回attr0，否则则返回attr1 */
select decode(0,1,0,1) from dual;
-- 1
select decode('0','0',0,1) from dual;
-- 0
```
# 对 null 的判断 
- MySQL ifnull
```sql
/* if(exp0,exp1)，如果exp0为null则返回exp1，如果exp0不为null则返回exp0 */
select ifnull(null,0);
-- 0
select ifnull(1,0);
-- 1
```
- Oracle nvl
```sql
/* nvl(exp0,exp1)，如果exp0为null则返回exp1，如果exp0不为null则返回exp0 */
select nvl(null,0) from dual;
-- 0
select nvl(1,0) from dual;
-- 1
```