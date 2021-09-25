---
layout: post
title: "按每行长度排序文本行"
date: 2016-01-20 10:14:15 +0800
comments: true
categories: Shell
---
I have a file containing quite many lines of strings and I want to sort them by line length. Here is how.

```sh
cat $file | awk '{ print length($0) " " $0; }' | sort -r -n | cut -d ' ' -f 2- | less
```
