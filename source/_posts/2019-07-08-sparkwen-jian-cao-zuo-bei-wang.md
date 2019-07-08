---
layout: post
title: "Spark文件操作备忘"
date: 2019-07-08 11:08:53 +0800
comments: true
categories: BigData
---
1. 读取一个文本文件，然后进行repartition:

```sh
spark.read.textFile(path1).repartition(1).write.text(path2)
```

2. pyspark 基本的dataframe的操作:

```py
from pyspark.sql import SparkSession
master = "local"

df = spark.read.parquet(raw_data)
df_filtered = df.select('f1', 'f2', 'f3', 'f4').filter((df['f1'] >= 1531670400) & (df['f1'] <= 1532188800) & (df['f2'] == 15) & (df['f3'] != '') & (df['f4'] > 0))

import pyspark.sql.functions as func
result = df_filtered.groupby(df['f3']).agg(func.countDistinct('f1'))

result.rdd.repartition(1).map(lambda row: str(row[0]) + "," + str(row[1])).saveAsTextFile(path2)
```

3. 用Spark错做数据

```scala
val diff = diff1.union(diff2)

val raw = spark.read.textFile(path1)

// 限定有3个字段, 存成df
val raw_df = raw.filter(x => x.split("\t").length == 3).map(x => (x.split("\t")(0), x.split("\t")(1).toLong, x.split("\t")(2))).toDF("f1", "f2", "f3")

// join获取rawdata
val joined_diff = diff.join(raw_df, diff("f1") === raw_df("f1") && diff("f2") === raw_df("f2"), "inner").toDF("f1", "f2", "f3", "f4", "f5", "f6")

// 存数据
val result_df = joined_diff.select($"f1", $"f2", $"f3", $"f4")
result_df.repartition(1).write.mode("overwrite").option("delimiter", "\t").csv(path2)
```
