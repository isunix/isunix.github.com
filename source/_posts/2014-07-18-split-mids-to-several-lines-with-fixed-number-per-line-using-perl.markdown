---
layout: post
title: "将一个每行一个item的多行文本转变成每行固定数目的item的文本(Perl)
"
date: 2014-07-18 21:38:16 +0800
comments: true
categories: Perl
---
事情是这样的，在工作中有许多的mids，想要贴到一个文本框中去，但是在进行reinjection后，是成每行一个mid的格式。我们想要把它们变成是每行给定数目的mids这样的格式， 方便贴到文本框中去. 之前用php实现过， 现在贴出来perl的版本的。

```perl

#usage：perl script.pl file.txt
use strict;
use warnings;
use utf8;


my $columns = $ARGV[1] || 8;
open(my $IN, "$ARGV[0]") or die "in: $@";
open(my $OUT, ">", "$ARGV[0].new") or die "out: $@";

while(chomp(my @lines = <$IN>)){

        for(my $i=1; $i <= @lines; $i++){
            my $t = $i - 1;
            print $OUT "$lines[$t]";
            if($i % $columns == 0){
                print $OUT "\n";
            }
        }
    }

close($IN);
close($OUT);


```