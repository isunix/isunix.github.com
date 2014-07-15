---
layout: post
title: "linux shell scripting cookbook 2nd notes"
date: 2014-06-19 09:39:37 +0800
comments: true
categories: shell
---
1. get the length of a variable:   

```bash
length=${#var}
```  

2. arguments:   

```
$1 is the first argument$2 is the second argument$n is the nth argument"$@"expands as "$1" "$2" "$3" and so on"$*" expands as "$1c$2c$3", where c is the first character of IFS"$@" is used more often than "$*"since the former provides all arguments as a single string

```