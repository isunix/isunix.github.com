---
layout: post
title: "some basics about generators in python"
date: 2015-10-19 08:46:43 +0800
comments: true
categories: Python
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


About how to use non-generator methods, generator methods, awk to calculate the sum of a columns of numbs.

The records in the log file looks like this:

```
156.63.68.202 - - [29/Feb/2008:07:49:28 -0600] "GET /favicon.ico HTTP/1.1" 404 133
80.161.85.77 - - [29/Feb/2008:07:52:46 -0600] "GET /ply/ply.html HTTP/1.1" 200 97238
```

First the non-generator method:

```py
wwwlog = open("access-log")
total = 0
for line in wwwlog:
    bytestr = line.rsplit(None,1)[1]
    if bytestr != '-':
        total += int(bytestr)

print "Total", total
```

and the generator method:

```py
wwwlog     = open("access-log")
bytecolumn = (line.rsplit(None,1)[1] for line in wwwlog)
bytes      = (int(x) for x in bytecolumn if x != '-')

print "Total", sum(bytes)
```

and then the awk method:

```awk
awk '{ total += $NF } END { print total }' access-log
```

PS: (a very useful shell script tutorial)

```html
http://www.grymoire.com/Unix/Sh.html
```
