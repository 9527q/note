# 日期和时间

## now、sysdate、sleep、current_timestamp

now() 和 sysdate() 都是获取日期+时间，不过前者是整个语句开始执行的时间，sysdate() 是实时获取当前时间。
current_timestamp() 和 now() 一样。
sleep(n) 返回 0。

```sql
mysql> select now(), sysdate(), sleep(3), now(), sysdate();
+---------------------+---------------------+----------+---------------------+---------------------+
| now()               | sysdate()           | sleep(3) | now()               | sysdate()           |
+---------------------+---------------------+----------+---------------------+---------------------+
| 2019-03-12 11:52:11 | 2019-03-12 11:52:11 |        0 | 2019-03-12 11:52:11 | 2019-03-12 11:52:14 |
+---------------------+---------------------+----------+---------------------+---------------------+
1 row in set (3.01 sec)

mysql> select sysdate(), sleep(3), now();
+---------------------+----------+---------------------+
| sysdate()           | sleep(3) | now()               |
+---------------------+----------+---------------------+
| 2019-03-12 11:52:31 |        0 | 2019-03-12 11:52:31 |
+---------------------+----------+---------------------+
1 row in set (3.00 sec)
```

## date_format、time_format、str_to_date

str_to_date 不能作用于只有时间的情况

%y | %Y | %m | %d | %H | %h | %i | %s
-|-|-|-|-|-|-
年19 | 年2019 | 月 | 日 | 时 | 时 | 分 | 秒

```sql
mysql> select date_format('2019-03-12 11:15:37', '%y-%m-%d-%H-%h-%i-%s');
+------------------------------------------------------------+
| date_format('2019-03-12 11:15:37', '%y-%m-%d-%H-%h-%i-%s') |
+------------------------------------------------------------+
| 19-03-12-11-11-15-37                                       |
+------------------------------------------------------------+
1 row in set (0.00 sec)

mysql> select time_format('2019-03-12 11:15:37', '%y-%m-%d-%H-%h-%i-%s');
+------------------------------------------------------------+
| time_format('2019-03-12 11:15:37', '%y-%m-%d-%H-%h-%i-%s') |
+------------------------------------------------------------+
| 00-00-00-11-11-15-37                                       |
+------------------------------------------------------------+
1 row in set (0.00 sec)

mysql> select str_to_date('08/09/2008', '%m/%d/%Y');
+---------------------------------------+
| str_to_date('08/09/2008', '%m/%d/%Y') |
+---------------------------------------+
| 2008-08-09                            |
+---------------------------------------+
1 row in set (0.00 sec)

mysql> select str_to_date('08.09.2008 08:09:30', '%m.%d.%Y %h:%i:%s');
+---------------------------------------------------------+
| str_to_date('08.09.2008 08:09:30', '%m.%d.%Y %h:%i:%s') |
+---------------------------------------------------------+
| 2008-08-09 08:09:30                                     |
+---------------------------------------------------------+
1 row in set (0.00 sec)
```

## to_days、from_days、time_to_sec、sec_to_time

```sql
mysql> select to_days('0001-02-01'), to_days(now()), from_days(700000), time_to_sec(now()), sec_to_time(800);
+-----------------------+----------------+-------------------+--------------------+------------------+
| to_days('0001-02-01') | to_days(now()) | from_days(700000) | time_to_sec(now()) | sec_to_time(800) |
+-----------------------+----------------+-------------------+--------------------+------------------+
|                   397 |         737495 | 1916-07-15        |              42454 | 00:13:20         |
+-----------------------+----------------+-------------------+--------------------+------------------+
1 row in set (0.00 sec)
```

## makdedate(year,dayofyear)，maketime(hour,minute,second)

```sql
mysql> select makedate(2019, 55), maketime(3,3,3);
+--------------------+-----------------+
| makedate(2019, 55) | maketime(3,3,3) |
+--------------------+-----------------+
| 2019-02-24         | 03:03:03        |
+--------------------+-----------------+
1 row in set (0.01 sec)
```

## Unix 时间戳、日期转换函数

```sql
unix_timestamp()  -- 当前时间戳
unix_timestamp(date)  -- 将日期/日期字符串转换成时间戳
from_unixtime(unix_timestamp)  -- 从时间戳转换为时间
from_unixtime(unix_timestamp,format)  -- 转换为时间并且指定样式
```

## date_add(datetime/datetime_str, interval num unit)，datesub()，adddate(), addtime()

unit：day、hour、minute、second、microsecond、week、month、quarter、year、

```sql
mysql> set @dt = now();
Query OK, 0 rows affected (0.01 sec)

mysql> select date_add(@dt, interval 1 day);
+-------------------------------+
| date_add(@dt, interval 1 day) |
+-------------------------------+
| 2019-03-16 14:45:24           |
+-------------------------------+
1 row in set (0.00 sec)

mysql> select date_add(@dt, interval '01:15:30' hour_second);
+------------------------------------------------+
| date_add(@dt, interval '01:15:30' hour_second) |
+------------------------------------------------+
| 2019-03-15 16:00:54                            |
+------------------------------------------------+
1 row in set (0.00 sec)
```

## datediff(date1, date2)，timediff(time1, time2)

## MySQL 时间戳（timestamp）转换、增、减函数：

```sql
timestamp(date) -- date to timestamp
timestamp(dt, time) -- dt + time
timestampadd(unit,interval,datetime_expr)
timestampdiff(unit,datetime_expr1,datetime_expr2)

select timestamp('2008-08-08'); -- 2008-08-08 00:00:00
select timestamp('2008-08-08 08:00:00', '01:01:01'); -- 2008-08-08 09:01:01
select timestamp('2008-08-08 08:00:00', '10 01:01:01'); -- 2008-08-18 09:01:01

select timestampadd(day, 1, '2008-08-08 08:00:00'); -- 2008-08-09 08:00:00
select date_add('2008-08-08 08:00:00', interval 1 day); -- 2008-08-09 08:00:00

MySQL timestampadd() 函数类似于 date_add()。
select timestampdiff(year,'2002-05-01','2001-01-01'); -- -1
select timestampdiff(day ,'2002-05-01','2001-01-01'); -- -485
select timestampdiff(hour,'2008-08-08 12:00:00','2008-08-08 00:00:00'); -- -12

select datediff('2008-08-08 12:00:00', '2008-08-01 00:00:00'); -- 7
```

## ySQL 时区（timezone）转换函数 convert_tz(dt,from_tz,to_tz)

```sql
select convert_tz('2008-08-08 12:00:00', '+08:00', '+00:00'); -- 2008-08-08 04:00:00
```