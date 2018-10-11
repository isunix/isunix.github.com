---
layout: post
title: "mastering perl learning notes"
date: 2014-09-06 18:03:53 +0800
comments: true
categories: Perl
---
This is for the book "mastering perl". There are some code snippets in this book which I think is quite useful, thus I keep a note of them below.  

1.global matching:  

```pl
$_ = "Just another Perl hacker,";my @words = /(\S+)/g; # "Just" "another" "Perl" "hacker,"
print join("",split(@words));
```  

2.my $word_count = () = /(\S+)/g;   
It will give out the number of matched items.

3.
