---
layout: post
title: "wget下载多个文件"
date: 2015-12-31 18:36:09 +0800
comments: true
categories: Shell
---
I want to down the lecture notes on the page 

```html
http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-001-structure-and-interpretation-of-computer-programs-spring-2005/lecture-notes/
```

Here is the command I am using.

```sh
wget http://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-001-structure-and-interpretation-of-computer-programs-spring-2005/lecture-notes/lecture{1..26}webhand.pdf
```

The sad thing is not all the sequences are consecutive.

