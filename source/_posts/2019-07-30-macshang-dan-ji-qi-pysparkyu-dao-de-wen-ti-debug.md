---
layout: post
title: "Mac上单机起PySpark遇到的问题debug"
date: 2019-07-30 10:38:15 +0800
comments: true
categories: BigData
---
今天在本地起个`pyspark` 发现总是遇到

```
Caused by: java.net.UnknownHostException: master: nodename nor servname provided, or not known
```
尝试了设置 `SPARK_HOME`, `HADOOP_HOME` 等变量之后，依然不起作用。

最后发现是要修改 `SPARK_HOME` 里面的配置文件`spark-env.sh`

```sh
export SPARK_MASTER_IP=StevenMac
export SPARK_LOCAL_IP=StevenMac
```

并且在`/etc/hosts` 文件中，加入如下的内容:

```sh
127.0.0.1  StevenMac
```
Bingo!!!



