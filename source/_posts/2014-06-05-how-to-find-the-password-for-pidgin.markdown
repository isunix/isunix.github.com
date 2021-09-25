---
layout: post
title: "命令行找到pidgin的密码"
date: 2014-06-05 20:49:16 +0800
comments: true
categories: Linux&Mac
---
Use the following command line to find the password for your account on pidgin:

```bash
cat $HOME/.purple/accounts.xml | grep pass
```
and it works.
