---
layout: post
title: "常用命令行"
date: 2015-11-02 16:21:57 +0800
comments: true
categories: Shell
---
We can use the following shell scripts to find the 10 most used shell commands for a user.

```sh
history | awk '{a[$2]++} END {for(i in a) {print a[i]" "i}}'| sort -rn | head
```
