---
layout: post
title: "怎么去除windows编辑过的文件中的^M字符"
date: 2016-07-18 08:12:34 +0800
comments: true
categories: Shell
---
We can use the following two methods to get rid of the "^M" character in a file which was edited on windows using vim.


1.

```sh
:%s/\r//g
```

2.

```sh
:%s/ctrl-v ctrl-m//g
```

The second one means pressing ctrl-v, then ctrl-m first.