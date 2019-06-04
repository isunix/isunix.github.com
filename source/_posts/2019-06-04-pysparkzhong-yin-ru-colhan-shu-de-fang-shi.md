---
layout: post
title: "pyspark中引入col函数的方式"
date: 2019-06-04 08:59:32 +0800
comments: true
categories: BigData
---
在python代码中通过 ``from pyspark.sql.functions import col`` 来引入 ``col`` 这个函数的时候，总是报错，找不到这个函数. 后来参考
<https://stackoverflow.com/questions/40163106/cannot-find-col-function-in-pyspark> 这个文章, ``pip install pyspark-stubs`` 再去引用就好了.

