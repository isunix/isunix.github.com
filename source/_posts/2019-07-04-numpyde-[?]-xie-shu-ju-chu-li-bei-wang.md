---
layout: post
title: "numpy的一些数据处理备忘"
date: 2019-07-04 11:43:34 +0800
comments: true
categories: Data&ML&AI
---
## 记录numpy中的一些数据处理的方法.

1. 比如我们通过如下的方式，获取到了iris的数据,

```py
import pandas as pd
import numpy as np
from sklearn.datasets import load_iris

iris = load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)

df.columns = ['sepal length', 'sepal width', 'petal length', 'petal width', 'label']
```

A. 如果我们想要去取第一列，第二列，和最后一列(label), 可以使用如下的方式:

```py
data = np.array(df.iloc[:100, [0, 1, -1]])
```

`df.shape` 是 `(150, 5)`, `data.shape` 是 `(100, 3)`

`data` 现在是`lists in list` 的一个`ndarray`

B. 如果我们想要去取`data`的每行的前两列， 还有最后一列，可以使用如下的方式:

```py
X, y = data[:, :-1], data[:, -1]
```

`X, y` 都是 ndarray. `x.shape` 是 `(100, 2)`, `y.shape` 是 `(100,)`

C. 如果要对标签进行二分类，我们可以使用 python 的 list comprehension:

```py
y = np.array([1 if i == 1 else -1 for i in y])
```

这样处理了之后，y 的 shape 还是跟之前是一样的.

2. 如果我们又一个ndarray, `an_ndarray = np.array([[11,12,13,14], [21,22,23,24], [31,32,33,34]])`

`row_rank1 = an_array[1, :]` 和 `row_rank2 = an_array[1:2, :]` 将会给出不同的结果，可以输出来看看有啥不同， 这个很重要.
`


