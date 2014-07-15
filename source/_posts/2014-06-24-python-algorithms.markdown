---
layout: post
title: "Python Algorithms"
date: 2014-06-24 15:23:46 +0800
comments: true
categories: Python
---
1.To test the time we used while execting something, we can issue the following command: 

```python

python -m timeit -s"import mymodule as m" "m.myfunction()"

```   

or separately: 

```python

import timeit
timeit.timeit("x = 2 + 2")
	
```   
