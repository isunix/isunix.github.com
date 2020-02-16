---
layout: post
title: "Python中不输出warning的信息"
date: 2019-07-29 13:36:53 +0800
comments: true
categories: Python
---
我们在`Python` 代码中，如果不想输出一些warnings, 可以在代码的一开始，加入如下的代码，就可以了.

```py
import warnings
warnings.filterwarnings('ignore')
```
filterwarnings 函数可以带参数的，上述的方式是把所有的warnings都给ignore了.
