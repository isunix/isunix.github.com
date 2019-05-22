---
layout: post
title: "linux命令ln的使用备忘"
date: 2019-05-22 16:22:49 +0800
comments: true
categories: Linux
---

我们现在在/usr/lib64中有个文件librpm.so.3.2.2, 我们想要在/usr/lib64做个软连接, 起名叫做librpm.so.3, 指向librpm.so.3.2.2, 我们可以这样做,

```cd /usr/lib64 && ln -s ln -s librpm.so.3.2.2 librpm.so.3```
