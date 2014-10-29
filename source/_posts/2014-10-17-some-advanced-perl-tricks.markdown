---
layout: post
title: "some advanced perl tricks"
date: 2014-10-17 18:50:35 +0800
comments: true
categories: 
---
I am taking notes of some of the advanced perl tricks used in perl.  

1.to get all the matched items using the /g flag,

```pl
$_ = "Just another Perl hacker,";my @words = /(\S+)/g; # "Just" "another" "Perl" "hacker,"
```

2.to get the word count, 

```pl
my $word_count = () = /(\S+)/g;
```

3.The built-in pos() operator returns the match position for the string we give it (or $_ by default).   

```pl
$_ = "just another perl hacker";
/(just)/g;
my $pos = pos();
print "[$1] ends at position $pos\n";
```  

4.To anchor our next match exactly where we left off the last time, we can use the \G anchor. It’s just like the beginning of string anchor \A, except for where \G anchors at the current match position. If our match fails, Perl resets pos() and we start at the beginning of the string.  
 

