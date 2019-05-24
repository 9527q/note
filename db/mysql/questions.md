# 常见问题

## 字段名和关键字重名

字段用  ``` ` ```（1旁边的那个）引起来

## 什么是utf8mb4？utf8 + emoji表情

```sql
create database oss_dev character set utf8mb4;
```

此处设置为utf8mb4会触发MySQL 5.7 默认的index prefix限制，须配合innodb_large_prefix=ON使用，不过应该是自动设置为ON了。

## error: 1449

导出数据库为 .sql 时报错：`Got error: 1449: The user specified as a definer ('oss'@'%') does not exist when using LOCK TABLES`

解决：

```sql
-- 1. 登陆数据库
-- $ msyql -u root -p
-- 2. 给权限（oss换成报错中提示的那个，passwd换成自己的密码）
mysql> grant all privileges on *.* to oss@"%" identified by "passwd";
Query OK, 0 rows affected, 1 warning (0.02 sec)

mysql> flush privileges;
Query OK, 0 rows affected (0.04 sec)

-- 3. 退出再次执行导出命令即可
```