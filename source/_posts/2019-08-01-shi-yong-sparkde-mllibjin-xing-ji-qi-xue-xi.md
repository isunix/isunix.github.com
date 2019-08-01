---
layout: post
title: "使用Spark的MLlib进行机器学习"
date: 2019-08-01 17:55:54 +0800
comments: true
categories: Data&ML&AI
---

1. 比如我们有个case class

```scala
case class CaseClassTest(user: String, name: String)
```

我们通过使用`mapPartitions`来进行操作， 注意此处`mapPartitions`的用法:

```scala
val mapResult = spark.read.textFile(input).map(_.split("\t")).mapPartitions {
      iter =>
        iter.map {
          iterms => CaseClassTest(iterms(0), iterms(1))
        }
    }
```



2. `reduceByKey` 和 `case` 的用法

   ```scala
   val data = gowalla.map {
         check: CheckIn => (check.user, (1L, Set(check.time), Set(check.location)))
       }.rdd.reduceByKey{
         case (left, right) => (left._1 + right._1, left._2.union(right._2),left._3.union(right._3))
       }.map{
         case (_, (checkins, days:Set[String], locations:Set[String])) =>
           Vectors.dense(checkins.toDouble, days.size.toDouble, locations.size.toDouble)
           //次数，天数，地点数
       }
   ```

   

`reduceByKey` 这里是求 `(1L, Set(check.time), Set(check.location))` 中的一个元素累加，第二个元素求并集，第三个元素也是求并集. `case` 的作用是让输入符合规范； 注意在 `map` 中，我们可以限定指示变量的类型， 比如这里的 `check: CheckIn =>`



#### 参考

1. Spark机器学习进阶实战