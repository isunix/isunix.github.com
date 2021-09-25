---
layout: post
title: "Perl中hash的使用"
date: 2014-07-18 19:18:44 +0800
comments: true
categories: Perl
---
1.要求用户输入人名， 打印出对应的item.

```perl

my %last_name = qw{
    fred flintstone
    barney rubble
    wilma flintstone
};

print "please enter a first name: ";
chomp(my $name = <STDIN>);
print "that's $name $last_name{$name}.\n";


```  
这是一个很典型的标准用法了。  

2.要求用户进行几行输入，然后统计频数.   

```perl
use strict;
use warnings;
use utf8;

my (@words, %count, $word);
chomp(@words = <STDIN>);

foreach $word (@words){
    $count{$word} += 1;
}

foreach $word (keys %count){
    print "$word was seen $count{$word} times.\n";
}

```