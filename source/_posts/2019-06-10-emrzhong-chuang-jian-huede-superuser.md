---
layout: post
title: "EMR中创建HUE的superuser"
date: 2019-06-10 17:48:43 +0800
comments: true
categories: BigData
---
想要在 EMR 中创建 HUE 的 superuser， 可以使用如下的方式

```sh
cd /usr/lib/hue/
sudo build/env/bin/hue  createsuperuser
```
