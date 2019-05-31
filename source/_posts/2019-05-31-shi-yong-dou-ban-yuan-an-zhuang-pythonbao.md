---
layout: post
title: "使用豆瓣源安装python包"
date: 2019-05-31 08:01:15 +0800
comments: true
categories: Python
---
我们在使用pip安装python的包的时候，可以使用豆瓣源来提高下载速度

```sh
pip  install  requests -i  https://pypi.doubanio.com/simple/  --trusted-host pypi.doubanio.com
```

在linux和mac上，我们可以在$HOME/.pip/pip.conf里面，写入如下的内容, 那样就不用每次都像上面那样写那么长的一大串了

```sh
[global]
index-url = https://pypi.doubanio.com/simple
[install]
trusted-host = pypi.doubanio.com
```
