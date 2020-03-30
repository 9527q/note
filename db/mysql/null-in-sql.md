![null-in-sql](./images/null-in-sql.png)

SQL 中的 NULL
============

（译自 [NULL Values in SQL Queries](https://mitchum.blog/null-values-in-sql-queries/)）

SQL 中的 NULL 到底是怎样一个概念呢？有什么要注意的吗？这篇文章就是要把它讲清楚。

### 查询某列值为 NULL 的数据

当想查询某一列值为 NULL 的数据时，下面两种哪个更好呢？

> SELECT * FROM SOME_TABLE
> **WHERE SOME_COLUMN <span style="color:red">=</span> NULL**

还是

> SELECT * FROM SOME_TABLE
> **WHERE SOME_COLUMN <span style="color:red">IS</span> NULL**

答案是，第二种更好。

为什么呢？为什么其他的比较都不用 **`IS`** 呢？比如想知道一个字段值是不是等于1，可以用一个简单的 `WHERE` 子句：

> WHERE SOME_COLUMN = 1

所以到底为什么对 NULL 区别对待使用 **`IS`** 呢？

因为：**在 SQL 中，NULL 表示「未知」的意思**，就是「未知」，不知道，不了解，未知！（原文：unknown）

### NULL 是「未知」

在大多数数据库中，NULL 和空字符串是有区别的。

但也有例外，比如在 Oracle 中，根本就不允许一个值是空字符串，Oracle 中所有的空字符串都会自动转换成 NULL。

不过对于其他大多数数据库来说，NULL 和空字符串是区别对待的：
- 空字符串也**是一种值**，只不过是**空的**而已。
- NULL **是一个「未知」值**。（或者说是「未知」，没有「值」的概念）

举个例子，就好像问：美国总统西奥多·罗斯福的中间名是什么？
- 一种回答可能是：我不知道西奥多·罗斯福的中间名是什么。（这种情况「中间名」字段就应该是 NULL）
- 还有一种回答可能是：西奥多·罗斯福没有中间名，他父母没给他起中间名，我知道的事实就是西奥多·罗斯福没有中间名。（这种情况「中间名」就应该为空字符串）

谨记 NULL 就是「**未知**」这个概念，就可以很容易处理一些使用 NULL 时可能遇到的麻烦。

比如下面的 WHERE 子句就会得到 true，那就能查到数据（如果数据库有数据的话）:

> SELECT * FROM SOME_TABLE
> **WHERE 1 = 1**

下面的子句会得到 false，永远都查不到数据：

> SELECT * FROM SOME_TABLE
> **WHERE 1 = 0**

而下面的 WHERE 子句会得到 NULL，因为数据库并不知道 1 和 NULL（「未知」）是什么关系，他们相等不相等，数据库不清楚，所以 WHERE 子句得到的又是 NULL（「未知」）。所以下面的查询永远也不会返回任何数据。

> SELECT * FROM SOME_TABLE
> **WHERE 1 = NULL**

### 三元逻辑（原文为 Ternary Logic）

一个 SQL 语句中 WHERE 子句有三种不同的结果
- **true**（会返回数据）
- **false**（不会返回数据）
- **NULL**（「未知」也不会返回数据）

好了，那既然 false 和 NULL 都不会返回数据，那干嘛还要关注它们的区别呢？

当遇上 NOT() 的时候就有问题了。

比如下面这个语句，1 肯定等于 1，显然经过 NOT() 后就会变成 false，那就永远不会返回数据。

> SELECT * FROM SOME_TABLE
> **WHERE NOT(1 = 1)**

下面这句呢，显然 NOT() 后会得到 true，当然会返回数据。

> SELECT * FROM SOME_TABLE
> **WHERE NOT(1 = 0)**

但是这句呢？

> SELECT * FROM SOME_TABLE
> **WHERE NOT(1 = NULL)**

上面这句 `1 = NULL` 由于数据库不知道 NULL 是什么，「未知」，所以其结果是 NULL。对 NOT() 来说呢，它也不知道 NULL 是什么，该怎么处理，所以也会返回 NULL，所以 WHERE 子句得到的是 NULL，既不是 true 也不是 false 而是 NULL，所以上面这条语句永远都**不会**返回数据。

那么好了，看下面这两条语句，虽然是相反的条件，但结果一致：都不会查询到数据。

> SELECT * FROM SOME_TABLE
> **WHERE NOT(1 = NULL)**

> SELECT * FROM SOME_TABLE
> **WHERE 1 = NULL**

### NOT IN 和 NULL

NOT IN 也是非常值得注意的。

比如下面这个 SQL，1 显然在后面的列表中，WHERE 就会得到 true，那么就会查询到数据。

> SELECT * FROM SOME_TABLE
> **WHERE 1 IN (1, 2, 3, 4, NULL)**

再看下面这句，显然 1 是在数组中的，那么 NOT IN 就会得到 false，那么就不能查询到数据。

> SELECT * FROM SOME_TABLE
> **WHERE 1 NOT IN (1, 2, 3, 4, NULL)**

再看这个：

> SELECT * FROM SOME_TABLE
> **WHERE 5 NOT IN (1, 2, 3, 4, NULL)**

先说答案：这句语句**不能**查询到数据。

5 在不在后面的列表中呢？数据库是不知道的，因为里面有个 NULL，谁知道 5 等不等于 NULL（「未知」），不知道，所以 `5 NOT IN (1, 2, 3, 4, NULL)` 得到的是 NULL，所以查询不到数据。

### 小结

以上，**NULL 就是 NULL，是「未知」**，这样一种概念的重要性就介绍完了。理解这一点，在构建复杂 SQL 时将很有用。
