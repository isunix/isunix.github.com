---
layout: post
title: "generate chapters at once"
date: 2014-07-17 10:47:48 +0800
comments: true
categories: Perl
---
I use this script to generate chapters at once. The number of chapters you want to generate in passed through the command line as the first argument.  

```perl 

use strict;
use warnings;
use utf8;
use Data::Dumper;

my $chap_num = $ARGV[0];

for(my $i = 1; $i <= $chap_num; $i++){
    mkdir "chap_$i";
}

```