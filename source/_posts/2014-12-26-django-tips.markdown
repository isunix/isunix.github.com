---
layout: post
title: "django tips"
date: 2014-12-26 15:43:22 +0800
comments: true
categories: Django
---
The following knowledge tips of Django need to be paid attention to.

1.parse_command_line

```py
DATABASE_ROUTERS
from tornado.options import parse_command_line
parse_command_line()
```

2.declare a class at runtime

```py
DynamicClass = type('DynamicClass', (), {'spam': 'eggs'})
```

3.