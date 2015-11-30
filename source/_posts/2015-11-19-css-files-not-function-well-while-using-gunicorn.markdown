---
layout: post
title: "css files not function well while using gunicorn"
date: 2015-11-19 16:42:04 +0800
comments: true
categories: django
---
I find that my bootstap files not working well while I am using gunicorn to start the app.

```sh
gunicorn --env DJANGO_SETTINGS_MODULE=myapp.settings myapp_management.wsgi --timeout 300 --workers=2 --pid gunicorn.pid -b 0:10000 --access-logfile=log/access_charts.log --error-logfile=log/error_charts.log --access-logformat '"%(h)s %(l)s %(u)s %(t)s "%(r)s" %(s)s %(b)s "%(f)s" "%(a)s" %(D)s %(p)s'
```

I find a solution for this:

```html
http://stackoverflow.com/questions/12800862/django-static-files-under-gunicorn
```

To summarize it here, add the following contents to the urls.py file.

```sh
from django.contrib.staticfiles.urls import staticfiles_urlpatterns


urlpatterns += staticfiles_urlpatterns()
```

