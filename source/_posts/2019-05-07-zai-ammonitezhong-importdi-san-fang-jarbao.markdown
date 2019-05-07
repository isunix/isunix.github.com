---
layout: post
title: "在ammonite中import第三方jar包"
date: 2019-05-07 16:54:15 +0800
comments: true
categories: scala 
---
### 我们在scala的repl中, 如果想要引入一个第三方的jar包, 可以使用如下的方式
```
:require joda-time-2.1.jar
```

### 而在ammonite中, 可以使用如下的方式
```
import $cp.`joda-time-2.1.jar`
```
