---
layout: post
title: "django shell usage"
date: 2015-10-23 16:50:03 +0800
comments: true
categories: Django
---

Let's say we have an app named "people" and that in our models.py file, we have the following model:

```py
from django.db import models
class Person(models.Model):
	name = models.CharField(max_length=50)
	age = models.IntegerField()
```

After synchronizing the db, before django 1.7, we issue:

```sh
python manage.py syncdb
```

After django1.7:

```sh
python manage.py makemigrations
python manage.py migrate
```

For django's shell, we can enter it by issuing the following command:

```sh
python manage.py shell
```

and then

```sh
>>>from people.models import Person
>>>Person.objects.create(name="steven", age="24")
>>>Person.objects.get(name="steven")
```

There are several ways to create an object:

```sh
a.  Person.objects.create(name="steven", age=24)
b.  p = Person(name="steve", age=24)
    p.save()

c.  p = Person(name="steven")
	p.age = 23
	p.save()

d.  Person.objects.get_or_create(name="steven", age=24)
```

There are more ways to get an object:

```sh
a.	Person.objects.all()
b.	Person.objects.all()[:10] #切片操作，获取10个人，不支持负索引，切片可以节约内存
c.	Person.objects.get(name=name) #{get是用来获取一个对象的，如果需要获取满足条件的一些人，就要用到filter}
d.	Person.objects.filter(name="abc") # 等于Person.objects.filter(name__exact="abc")
e.	Person.objects.filter(name__iexact="abc") #{不区分大小写}
f.	Person.objects.filter(name__contains="abc") # 名称中包含 "abc"的人
g.	Person.objects.filter(name__icontains="abc") #名称中包含 "abc"，且abc不区分大小写
h.	Person.objects.filter(name__regex="^abc") # 正则表达式查询
i.	Person.objects.filter(name__iregex="^abc")# 正则表达式不区分大小写
j.	Person.objects.exclude(name__contains="WZ") # 排除包含 WZ 的Person对象
k.	Person.objects.filter(name__contains="abc").exclude(age=23) # 找出名称含有abc, 但是排除年龄是23岁的
```
























