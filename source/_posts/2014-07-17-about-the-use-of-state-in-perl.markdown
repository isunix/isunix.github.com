---
layout: post
title: "Perl中state的用法"
date: 2014-07-17 16:02:20 +0800
comments: true
categories: Perl
---
算了还是引用一下<<learning perl>>中文翻译版本中的话吧:   

```
在Perl中可以使用my操作符来创建私有变量， 但是每次调用这个子程序的时候，这个私有变量都会被重新定义。而使用state操作符来声明的变量，我们便可以在子程序的多次调用期间保留变量之前的值， 并将变量的作用域限于子程序内部

```

让我们来看下使用my还有使用state所产生的不同的效果吧。  

首先是my:  

```perl

use 5.010;

running_sum( 5, 6 );
running_sum( 1..3 );
running_sum( 4 );

sub running_sum {
    my $sum = 0;
    my @numbers;

    foreach my $number ( @_ ) {
      push @numbers, $number;
      $sum += $number;
    }

    say "the sum of (@numbers) is $sum";
}  

```  

这段code产生的结果是:  

```perl

the sum of (5 6) is 11
the sum of (1 2 3) is 6
the sum of (4) is 4

```   

下面是state:  

```perl

use 5.010;
running_sum( 5, 6 );
running_sum( 1..3 );
running_sum( 4 );

sub running_sum {
    state $sum = 0;
    state @numbers;
    foreach my $number ( @_ ) {
        push @numbers, $number;
        $sum += $number;
    }

say "The sum of (@numbers) is $sum";
}

```  
它的结果是:   

```perl  

The sum of (5 6) is 11
The sum of (5 6 1 2 3) is 17
The sum of (5 6 1 2 3 4) is 21

```