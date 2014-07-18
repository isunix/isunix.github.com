---
layout: post
title: "interesting use of state in perl"
date: 2014-07-17 18:48:44 +0800
comments: true
categories: Perl
---
还是来自<<learning perl>>中的例子。

1. 写一个名为greet的子例程，当给定一个人名作为参数的时候，打出欢迎他的信息，并告诉他前一个来宾的名字。  

```perl

use 5.010;
greet('Fred');
greet('Barney');

sub greet{
    state $last_person;

    my $name = shift;

    print "Hi, $name!";

    if (defined $last_person) {
        print "$last_person is also here!\n";
    }

    else {
        print "you are the first one here!\n";
    }

    $last_person = $name;
} 

```  
2.修改程序1， 告诉所有新来的人之前已经迎来了哪些人.   

```perl 
use Data::Dumper;
use 5.010;

greet('Fred');
greet('Barney');
greet('Wilma');
greet('Betty');

sub greet{
    state @before;

    my $name = shift;
    print "Hi, $name!";

    if (@before){
        print " I have seen @before\n";
    }
    else {
        print " you are the first one here!\n";
    }

    push @before, $name;
}

```