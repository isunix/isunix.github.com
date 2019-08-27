---
layout: post
title: "Spark中排序输出"
date: 2019-08-27 10:11:02 +0800
comments: true
categories: Data&ML&AI
---

```python
# initialize pyspark
import pandas as pd
import numpy as np
import json
np.set_printoptions(suppress=True)

import findspark
findspark.init()
import pyspark

from pyspark.sql import SparkSession
spark = SparkSession.builder \
    .appName('PySpark-Analysis') \
    .config("spark.executor.memory", "3g") \
    .config("spark.executor.cores", "8") \
    .getOrCreate()


import os
folder = "xxxx"
filename = "one-big.tsv"
file = os.path.join(folder, filename)

df = spark.read.text(file).rdd.map(lambda r: r[0]).map(lambda line: line.split("\t")).toDF()

df.orderBy("_1", "_2").coalesce(1).write.csv("xxx2", sep='\t')
```

