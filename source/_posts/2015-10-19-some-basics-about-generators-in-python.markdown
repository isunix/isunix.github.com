---
layout: post
title: "some basics about generators in python"
date: 2015-10-19 08:46:43 +0800
comments: true
categories: python 
---
Here below is a reference for learning python generators:

```html
http://www.dabeaz.com/generators/
http://www.dabeaz.com/finalgenerator/
http://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do-in-python/231855#231855
```

A basic explanation about the "for" statement in python:

```py
for x in obj:
	#statements
```

and how it is realized:

```py
_iter = iter(obj)
while 1:
	try:
		x = _iter.next()
	except StopIteration:
		break
	#statements
```

and why the "StopIteration" in the above code? It happens in iterables:

```py
>>> items = [1,2,3]
>>> it = iter(items)
>>> it.next()
1
>>> it.next()
2
>>> it.next()
3
>>> it.next()
Traceback (most recent call last):
  File "<input>", line 1, in <module>
StopIteration
>>>
```

and now will implement a user defined object that supports iterable:

```py
class countdown(object):
    def __init__(self, start):
        self.count = start

    def __iter__(self):
        return self

    def next(self):
        if self.count <= 0:
            raise StopIteration
        r = self.count
        self.count -= 1
        return r

if __name__ == '__main__':
    c = countdown(3)
    for i in c:
        print(i)
```

countdown using generator:

```py
def countdown(n):
    while n > 0:
        yield n
        n -= 1

for i in countdown(5):
    print(i)

```
