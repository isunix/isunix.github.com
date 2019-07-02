---
layout: post
title: "Zeppelin搭配Presto"
date: 2019-06-10 17:57:13 +0800
comments: true
categories: BigData
---
参考文章

``https://stackoverflow.com/questions/35858606/presto-interpreter-in-zeppelin-on-emr``

- 在 master 机器上安装 jdbc
```sh
sudo /usr/lib/zeppelin/bin/install-interpreter.sh --name jdbc
```

```sh
sudo stop zeppelin
sudo start zeppelin
```
