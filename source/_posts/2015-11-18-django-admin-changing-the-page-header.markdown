---
layout: post
title: "Django Admin: Changing the Page Header"
date: 2015-11-18 16:58:31 +0800
comments: true
categories: django
---
This post shows how to change the header of the django admin page.

The blog for reference is:

```html
http://www.mc706.com/tip_trick_snippets/42/django-admin-changing-the-page-header/
```
I will summarize its steps here:

1.Make sure the "TEMPLATE_DIRS" setup is correct(under the project's root directory):

```py
TEMPLATE_DIRS = (os.path.join(os.path.dirname(__file__), '..', 'templates').replace('\\','/'),)
```

2.create "admin" directory in the "templates" dir

3.In "templates/admin" directory, create the file "base_site.html".

4.Put the following things to the file "templates/admin/base_site.html" and modify it to suit your own usage.

```html
{% extends "admin/base.html" %}
{% load i18n %}

{% block title %}{{ title }} | {% trans 'Your title here' %}{% endblock %}

{% block branding %}
<h1 id="site-name">{% trans 'New Header Here' %}</h1>
{% endblock %}

{% block nav-global %}{% endblock %}
```

Refresh the amdin page and now you will see what you have updated.