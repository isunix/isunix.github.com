---
layout: post
title: "Perl中单行或者多行输出结果"
date: 2014-07-17 15:14:23 +0800
comments: true
categories: Perl
---
我们在标准输入中得到多行的值， 现在我们想要以单行还有多行的结果来把它们给显示出来， 要是想单行显示的话，可以如下:

```perl

chomp(@lines = <STDIN>);
@sorted = sort @lines;
print "@sorted\n"

```

多行的话可以:  

```perl 

print sort <STDIN>;

```  

这里的关键的地方就是chomp这个函数。