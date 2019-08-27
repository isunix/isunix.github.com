---
layout: post
title: "如何查看Linux中的内存占用情况"
date: 2019-08-27 11:17:03 +0800
comments: true
categories: Linux&Mac
---

```shell
ps -o pid,user,%mem,command ax | awk '($3 > 0){print}' | sort -b -k3 -r
```

可以使用如上的命令来看那些占用了内存的程序，并且排序.

也可以将上上面的命令搞成一个alias:

```shell
alias memcheck="ps -o pid,user,%mem,command ax | awk '(\$3 > 0){print}' | sort -b -k3 -r"
```

