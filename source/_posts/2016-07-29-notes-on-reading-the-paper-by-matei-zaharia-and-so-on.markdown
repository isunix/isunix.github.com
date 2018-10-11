---
layout: post
title: "notes on reading the paper by Matei Zaharia and so on"
date: 2016-07-29 11:52:31 +0800
comments: true
categories: Spark
---
This post keeps note for the paper "Resilient Distributed Datasets: A Fault-Tolerant Abstraction for In-Memory Cluster Computing" by Matei Zaharia and so on.

1.

```
Spark exposes RDDs through a language-integrated API where each dataset is represented as an object and transformations are invoked using methods on these objects.
```

2.

```
Programmers start by defining one or more RDDs through transformations on data in stable storage (e.g., map and filter). They can then use these RDDs in actions, which are operations that return a value to the application or export data to a storage system. Examples of actions include count (which returns the number of elements in the dataset), collect (which returns the elements themselves), and save (which outputs the dataset to a storage system)
```

3.

```
Spark computes RDDs lazily the first time they are used in an action, so that it can pipeline transformations
```

4.

```
In addition, programmers can call a persist method to indicate which RDDs they want to reuse in future operations. Spark keeps persistent RDDs in memory by default, but it can spill them to disk if there is not enough RAM.
```

5.

```
RDDs themselves are statically typed objects parametrized by an element type. For example, RDD[Int] is an RDD of integers.
```

6.

```
Transformations are lazy operations that define a new RDD, while actions launch a computation to return a value to the program or write data to external storage.
```

7.

```
map is a one-to-one mapping, while flatMap maps each input value to one or more outputs (similar to the map in MapReduce).
```

8.

```
Operations such as groupByKey, reduceByKey and sort automatically result in a hash or range partitioned RDD
```

9.

```
We found it both sufficient and useful to classify dependencies into two types: narrow dependencies, where each partition of the parent RDD is used by at most one partition of the child RDD, wide dependencies, where multiple child partitions may depend on it. For example, map leads to a narrow dependency, while join leads to to wide dependencies (unless the parents are hash-partitioned).
```