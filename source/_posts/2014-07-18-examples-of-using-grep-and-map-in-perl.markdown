---
layout: post
title: "Perl中的grep和map的使用"
date: 2014-07-18 20:55:08 +0800
comments: true
categories: Perl
---
在<<Learnign Perl>>中，初步介绍了perl的一些高级用法， 我之前翻译了些intermediate perl, 但是最近这段时间实在是太忙了， 而且现在还有很多其他的事情得去处理，所以真的不知道得到什么时候才可以继续拾起翻译intermediate perl的任务来。好了，下面把学习perl中的一些关于map还有grep的例子记录在这里，也方便自己以后来查询。   

```perl
my @odd_numbers = grep { $_ % 2 } 1..1000;  

my @matching_lines = grep { /\bfred\b/i } <$fh>;

my @matching_lines = grep /\bfred\b/i, <$fh>;  

my @matching_lines = grep /\bfred\b/i, <$fh>;
my $line_count = @matching_lines;  


my $line_count = grep /\bfred\b/i, <$fh>;  


my @data = (4.75, 1.5, 2, 1234, 6.9456, 12345678.9, 29.95);
my @formatted_data = map { &big_money($_) } @data;  


print "The money numbers are:\n",
map { sprintf("%25s\n", $_) } @formatted_data;  


my @data = (4.75, 1.5, 2, 1234, 6.9456, 12345678.9, 29.95);
print "The money numbers are:\n",
map { sprintf("%25s\n", &big_money($_) ) } @data;  


print "Some powers of two are:\n",
map "\t" . ( 2 ** $_ ) . "\n", 0..15;  

```