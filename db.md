# 数据库 datebase

## SQL

从表中删除数据（不释放空间）

```sql
DELETE FROM table_name [WHERE Clause]
```

### 函数

concat

## MySQL

[导入很大（> 1G）的 SQL 数据的方法](https://stackoverflow.com/questions/13717277/how-can-i-import-a-large-14-gb-mysql-dump-file-into-a-new-mysql-database)

导入大 SQL 时可能出现提示信息为“超时”/“变量不能为空”的错误，上面是解决方案。其中一个重点是关闭外键检查，可以大大降低所需时间，不过如果不是数据量非常大的话，光用方案中另外两个设置就足够了。
