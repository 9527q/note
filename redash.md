# Redash


筛选 `::filter`：在查询结果的某个字段上加一个筛选，类似 Excel，不过是单选的

```SQL
select
    name as '姓名::filter'
from student
```