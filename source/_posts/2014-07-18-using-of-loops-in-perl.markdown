---
layout: post
title: "Perl中循环的使用"
date: 2014-07-18 19:59:02 +0800
comments: true
categories: Perl
---
<<Learning Perl>>中的一个例子。  

```
Make a program that will repeatedly ask the user to guess a secret number
from 1 to 100 until the user guesses the secret number. Your program should pick
the number at random by using the magical formula int(1 + rand 100).§ When
the user guesses wrong, the program should respond, “Too high” or “Too low.” If
the user enters the word quit or exit, or if the user enters a blank line, the program
should quit. Of course, if the user guesses correctly, the program should quit then
as well!
```  

还是把code贴在这里吧！ 

```perl

my $secret = int(1 + rand(100));

while(1){
    print "please enter a guess from 1 to 100: ";
    chomp(my $guess = <STDIN>);
    if ($guess =~ /quit|exit|\A\s*\z/i){
        print "sorry you gave up, the number was $secret.\n";
        last;
    } elsif ($guess < $secret){
        print "too small!\n";
    } elsif ($guess == $secret){
        print "that was it!\n";
        last;
    } else {
        print "too large!\n";
    }
}  

```