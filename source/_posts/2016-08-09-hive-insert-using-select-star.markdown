---
layout: post
title: "hive insert using select *"
date: 2016-08-09 09:34:49 +0800
comments: true
categories: BigData
---
I want to insert into a table with values from another table. and I want to use the follwing statements,


```sql
insert into table table_a select * from table_b;
```

Both table_a and table_b have the followig 3 fields, "name", "age", and the "load_day" field which is used to partition.

If using the above syntax, we will get errors saying table has just 2 fields and table_b has 3.

So one right way to insert the data is:

```sql
insert into table table_a(partition="2016-08-01") select name, age from table_b where load_day = "2016-08-01"
```

What if there are many fields, thus we will need to list them one by one after select which is very tedious.

Here is the solution,

```sql
set hive.exec.dynamic.partition.mode=nonstrict;
insert into table table_a partition(load_day) select * from table_b;
```
