---
layout: post
title: "about the use of my and our in perl"
date: 2014-07-24 19:32:11 +0800
comments: true
categories: Perl
---
关于perl中的my， our，local的用法自己一直都是一知半解的。以至于基本上在程序中把所有的变量的前面都加上my， 省事还不报错!   

I am still not familiar the concept, but I will list some examples here to add as a reminder.  

```perl   
our $var = 1;
{
	our $var = 2;
	print "$var\n";
}
print "$var\n";    
```

It will give us the result:  

```
2
2
```  
If the code looks like this:   

```perl   
my $var = 1;
{
	my $var = 2;
	print "$var\n";
}
print "$var\n";    
```   
It will give us the result:   

```  
2
1  
```
If the code is:   

```perl  
our $var = 1;
{
	my $var = 2;
	print "$var\n";
}
print "$var\n";    
```     
It will give us the following result:  

```
2
1
```
if the code is:  

```perl 
my $var = 1;
{
	our $var = 2;
	print "$var\n";
}
print "$var\n";    
```  
It will give us the result:   

``` 
2
1
```
