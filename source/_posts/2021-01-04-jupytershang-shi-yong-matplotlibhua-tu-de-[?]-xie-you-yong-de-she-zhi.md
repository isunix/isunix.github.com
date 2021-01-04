---
layout: post
title: "jupyter上使用matplotlib画图的一些有用的设置"
date: 2021-01-04 09:41:29 +0800
comments: true
categories: Data&ML&AI

---
我们在mac上使用jupyter的时候，用matplotlib画图，产出的图形的质量不是很高，可以在如下的文件中, 加上设置:

`~/.ipython/profile_default/ipython_kernel_config.py`


```py
c.IPKernelApp.matplotlib ='inline' 
c.InlineBackend.figure_format ='retina'
```

默认的matplotlib画图的样式不是很美观， 我们可以做出如下的设置:

`plt.style.use('seaborn')`

我们可以使用如下的命令查看都有哪些可供选择的style

`plt.style.available`
