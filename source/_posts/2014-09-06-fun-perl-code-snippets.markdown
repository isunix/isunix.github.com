---
layout: post
title: "有趣的Perl代码片段"
date: 2014-09-06 10:02:29 +0800
comments: true
categories: Perl
---
I collect some useful code snippets here for later usage or just keep a note of what I have read.  

1.find files larger than a specifed size(in byte):   

```pl
use File::Find;
find(sub { print "$_\n" if -s $_ > $ARGV[0]; }, ".");
```  
2.we can use "man module::name" or "perldoc module::name" to check the detailed info of a module.   

3.For the first example, if using require, we can write it as the following:  

```pl
require File::Find;
File::Find::find(sub { print "$File::Find::name\n" if -s > 1_024_000; }, '.');
```  

4."use" happens during compile time, whereas "require" happens at runtime.    



