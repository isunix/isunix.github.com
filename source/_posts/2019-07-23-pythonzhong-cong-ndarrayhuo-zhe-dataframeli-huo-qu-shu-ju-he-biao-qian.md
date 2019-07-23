---
layout: post
title: "Python中从ndarray或者DataFrame里获取数据和标签"
date: 2019-07-23 11:27:22 +0800
comments: true
categories: Data&ML&AI
---
如果我们有一个ndarray, 最后一列是label，前面几列是data, 我们可以通过如下的方式去获取数据(假如我们有9列):
```py
X = dataset[:,0:-1] or X = dataset[:,0:8]
Y = dataset[:,8]
```

如果我们有个DataFrame, 我们可以通过如下的方式去获取:
```py
X, y = data.iloc[:,:-1], data.iloc[:,-1]
```


