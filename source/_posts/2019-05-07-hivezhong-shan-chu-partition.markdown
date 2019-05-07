---
layout: post
title: "hive中删除partition"
date: 2019-05-07 17:25:48 +0800
comments: true
categories: hive
---
```hive
alter table xxx drop PARTITION (partition_name<='2019-01-13');
```