---
title: Oracle 查看锁
translate_title: Oracle 查看锁
comments: false
date: 2016-08-10 10:34:00
categories:
  - Oracle
tags:
  - SQL
  - Oracle
---
Oracle 查看锁
==========

### 相关表
- v$lock
- v$sqlarea
- v$session
- v$process
- v$locked_object
- all_objects
- v$session_wait  

### 查看被锁的和具体的操作用户信息

```sql
select
  do.owner,
  do.object_name,
  lo.session_id,
  lo.locked_mode,
  s.username,
  s.sid,
  s.serial#,
  s.username,
  s.osuser,
  s.machine,
  s.terminal,
  s.program,
  s.action,
  s.logon_time
from
  v$locked_object lo, dba_objects do, v$session s
where
  do.object_id = lo.object_id and lo.session_id = s.sid
```

### 杀死进程

```sql
# sid + serial
alter system kill session [sid,serial#];
```
