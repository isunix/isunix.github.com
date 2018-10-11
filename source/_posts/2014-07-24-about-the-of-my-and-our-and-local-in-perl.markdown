---
layout: post
title: "about the use of my and our in perl"
date: 2014-07-24 19:32:11 +0800
comments: true
categories: Perl
---
关于perl中的my， our的用法自己一直都是一知半解的。以至于基本上在程序中把所有的变量的前面都加上my， 省事还不报错!   

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

If the code is one of the following, it will give us the result 2:  

```perl  
my $var = 1;
my $var = 2;
print $var, "\n";  

our $var = 1;
our $var = 2;
print $var, "\n";     

my $var = 1;
our $var = 2;
print $var, "\n";   

our $var = 1;
my $var = 2;
print $var, "\n"; 
```   
I still can not claim I understand my and our.   

We will give more examples on this.  

The following 3 code snippets will give us the result (1, 6, 11):   

```perl

my $i = 0;
for ($i = 1; $i<10; $i++){
    print $i, "\n";
    $i = $i + 4;
}
print $i, "\n";
#1,6,11   

our $i = 0;
for ($i = 1; $i<10; $i++){
    print $i, "\n";
    $i = $i + 4;
}
print $i, "\n";
#1,6,11   

our $i = 0;
for (our $i = 1; $i<10; $i++){
    print $i, "\n";
    $i = $i + 4;
}

print $i, "\n";
#1,6,11   
```  

While the following 3 will give us the result (1, 6, 0):  

```perl  

my $i = 0;
for (my $i = 1; $i<10; $i++){
    print $i, "\n";
    $i = $i + 4;
}
print $i, "\n";
#1,6,0


my $i = 0;
for (our $i = 1; $i<10; $i++){
    print $i, "\n";
    $i = $i + 4;
}
#1,6,0  

our $i = 0;
for (my $i = 1; $i<10; $i++){
    print $i, "\n";
    $i = $i + 4;
}
print $i, "\n";
#1,6,0  

```

