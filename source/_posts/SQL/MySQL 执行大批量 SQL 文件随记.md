---
title: MySQL 执行大批量 SQL 文件随记
translate_title: MySQL 执行大批量 SQL 文件随记
comments: false
date: 2016-09-25 12:13:00
categories:
  - MySQL
tags:
  - MySQL
---
MySQL 执行大批量 SQL 文件随记
==========
#### navicat 导出后导入报错 `1067 - Invalid default value for '字段名'`

```sql
-- 直接在 SQL 文件最前面加入以下内容
-- explicit_defaults_for_timestamp 变量, 默认为 OFF
-- 在导出的sql文件的开头加上 set explicit_defaults_for_timestamp = 'ON';
-- show global variables like '%explicit_defaults_for_timestamp%';
set explicit_defaults_for_timestamp = 'ON';
```

##### navicat 导入大sql文件报错 `2006 - MySQL server has gone away`

```sql
-- 直接在 SQL 文件最前面加入以下内容
-- show global variables like '%explicit_defaults_for_timestamp%';
set max_allowed_packet = 1073741824;
-- 如果无权限执行，可能更换高权限账号或者提高权限
-- set global max_allowed_packet = 1073741824;
set global max_allowed_packet = 1073741824;
```