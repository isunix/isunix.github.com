---
layout: post
title: "update all python modules through pip"
date: 2016-03-31 16:32:49 +0800
comments: true
categories: Python
---
I want to update all the installed python modules through pip. Here below is one recipe I found.

```py
import pip
from subprocess import call

for dist in pip.get_installed_distributions():
    call("pip install --upgrade " + dist.project_name, shell=True)
```

