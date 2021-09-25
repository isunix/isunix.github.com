---
layout: post
title: "Perl中sort函数的使用"
date: 2014-06-22 12:31:50 +0800
comments: true
categories: Perl
---
In Perl, function sort() sort the item of an array according to its corresponding acssci code. for example, if we have an array @array = (1, 3, 10, 2, 21) and use sort against this array, we will get the following result: 1 10 2 21 3. However if we want to sort these numbers according to its value, we can use the following method:   

```perl

sort{$a <=> $b} @array;   #ascending

sort{$b <=> $a} @array;   #descending

```