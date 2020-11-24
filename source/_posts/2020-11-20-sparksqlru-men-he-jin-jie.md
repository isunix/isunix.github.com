---
layout: post
title: "SparkSQL入门和进阶"
date: 2020-11-20 22:08:55 +0800
comments: true
categories: Data&ML&AI
---
## 常用的函数：

`select`、`lit`、`as`、`groupBy`、`agg`、`sum`、`as`、`where`、`withColumn`、 `col`、 `when`、 `otherwise`、 `join`、`withColumnRenamed`、 `isin`、 `cast`、 `$`、 `union`、 `gt`、 `struct`、`sort`、`desc`、`show`、`orderBy`、`asc`、`repartition`、`sortWithinPartitions`、`filter`、`selectExpr`、`pivot`、`expr`、`row_number`、`over`、 `partitionBy`


```scala
df
.select($"id",lit(1).as("cnt")) 
.groupBy("idd") 
.agg(sum("cnt").as("total"))
.where("total >=" + cnt2) 
.select("uid","total")

```
   

## UDF：

`spark.udf.register
`

## 参考链接:
- [SparkSQL DSL开发
](https://blog.csdn.net/weixin_40652340/article/details/79207455
)
- [Column](http://spark.apache.org/docs/latest/api/scala/org/apache/spark/sql/Column.html
)
- [Dataset](http://spark.apache.org/docs/latest/api/scala/org/apache/spark/sql/Dataset.html
)
- [functions](http://spark.apache.org/docs/latest/api/scala/org/apache/spark/sql/functions\$.html
)
- [sql](http://spark.apache.org/docs/latest/api/scala/org/apache/spark/sql/index.html\#DataFrame=org.apache.spark.sql.Dataset\[org.apache.spark.sql.Row\]
)
- [Scalar User Defined Functions (UDFs)
](https://spark.apache.org/docs/latest/sql-ref-functions-udf-scalar.html
)
- [SparkSQL DSL 随便写写](https://www.cnblogs.com/Diyo/p/11410895.html
)
- [SparkSQL案例------用SQL和DSL两种语法格式，求出用户连续登录天数
](https://blog.csdn.net/weixin_42419342/article/details/108918139?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~sobaiduend\~default-2-108918139.nonecase&utm_term=sparksql中dsl&spm=1000.2123.3001.4430
)