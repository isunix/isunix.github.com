---
layout: post
title: "numpy的一些数据处理备忘"
date: 2019-07-04 11:43:34 +0800
comments: true
categories: Data&ML&AI
---
## 记录numpy中的一些数据处理的方法.

- 比如我们通过如下的方式，获取到了iris的数据,

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

- 如果我们又一个ndarray, `an_ndarray = np.array([[11,12,13,14], [21,22,23,24], [31,32,33,34]])`

`row_rank1 = an_array[1, :]` 和 `row_rank2 = an_array[1:2, :]` 将会给出不同的结果，可以输出来看看有啥不同， 这个很重要.

- 我们也可以使用如下的方式，对array中的元素进行判断

```py
an_ndarray = np.array([[11,12], [21, 22], [31, 31]])
bigger_than_fifteen = (an_array > 15)
an_ndarray[bigger_than_fifteen]
```

或者我们也可以直接如下操作:

```py
an_ndarray[(an_ndarray > 15)]
```

- 下面是针对上面的`an_ndarray`进行的一些数学操作

```py
# 求各个元素的均值
an_ndarray.mean()

# 求每行的均值
an_ndarray.mean(axis=1)

# 求每列的均值
an_ndarray.mean(axis=0)

# 求所有元素的和
an_ndarray.sum()

# 求每行的中位数
np.median(an_ndarray, axix=1)

# 求每列的中位数
np.median(an_ndarray, axix=0)

# 想要找到unique的元素
np.unique(an_ndarray)

# 下面是一些集合的操作
s1 = np.array(['desk','chair','bulb'])
s2 = np.array(['lamp','bulb','chair'])
(s1, s2)

# s1 和 s2 交集
np.intersect1d(s1, s2)

# s1 和 s2 去重并集
np.union1d(s1, s2)

# 在s1然后不在s2中的元素
np.setdiff1d(s1, s2)

# 判断s1中的元素是不是在s2中
np.in1d(s1, s2)
```

- 广播
最好的操作方式是能打印出来看看长啥样.

- 文件的存取

```py
x = np.array([ 23.23, 24.24])
np.save('an_array', x)
np.load('an_array.npy')

np.savetxt('array.txt', X=x, delimiter=',')
np.loadtxt('array.txt', delimiter=',')
```

- 拼接数据集

```py
K = np.random.randint(low=2,high=50,size=(2,2))
M = np.random.randint(low=2,high=50,size=(2,2))

np.vstack((K,M))
np.hstack((K,M))

np.concatenate([K, M], axis = 0)
np.concatenate([K, M.T], axis = 1)

# vstack 和 hstack 和  最下面的两种方式是等价的
```
