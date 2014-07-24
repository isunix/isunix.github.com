---
layout: post
title: "about the sort function in perl"
date: 2014-07-24 16:51:22 +0800
comments: true
categories: Perl
---
This blog post is about the sort function in Perl. Mostly it is from the book "perl for dummies", since I am reading it now.   

This is a good book, since it explains many concepts very clearly.  

The "sort" function sorts a list alphabeticlly. Perl also allows us to sort a list according to the rule we defined.  

if alphabetically, we can write the code as the following:  

```perl

@strs = ('cognition', 'attune', 'bell');
print join(' ', sort @strs);

```    
It will give the following result:  

```
attune bell cognition
```


Here below I will show what we can do if we want to sort based on the way we want it to be:  

```perl 

@strs = ('cognition', 'attune', 'bell');
print join(' ', sort{length($a) <=> length($b)} @strs);  

```  
The above code will sort the list according to the length of the string in the list.  

What if the our so-called rule is a subroutine?  

```perl
sub lensort { length($a) <=> length($b) };

@strs = ('cognition', 'attune', 'bell');
print join(' ', sort lensort @strs);
 
```  

This post is going to be continued. I will add more things as I come accross more useful and interesing examples regarding the sort function.  




