---
layout: post
title: "installing from multiple requirements files"
date: 2015-09-21 16:18:23 +0800
comments: true
categories: Python
---
Say we want to install modules from multiple requirement files. We will put the requirement files in the directory "requirements".

First the base.txt file.

```
Django==1.7.10
psycopg2==2.4.5
```

Then the file local.txt

```
-r base.txt
django-discover-runner==0.2.2
```

and production.txt(production installaions should be close to what is used in other locations, so production.txt commonly just calls base.txt)

```
-r base.txt
```

The for local and production env, we can issue the following commands:

```sh
pip install -r requirements/local.txt
```

```sh
pip install -r requirements/production.txt
```
