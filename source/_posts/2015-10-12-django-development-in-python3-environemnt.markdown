---
layout: post
title: "django development in python3 environemnt"
date: 2015-10-12 14:55:22 +0800
comments: true
categories: Django
---
What if I want to development a django app in python3 environement.

Using vitualenv

```sh
python3 -m venv sbenv
source sbenv/bin/activate
pip install -r requirements.txt

```

Using virtualenvwrapper

```sh
which python3   --to get the location of python3 interpreter
mkvirtualenv --python=/usr/local/bin/python3 django_dev
workon django_dev
```
