---
layout: post
title: "notes on the book perl-debugged"
date: 2014-07-25 15:25:02 +0800
comments: true
categories: Perl
---
这篇blog是Perl debugged的阅读笔记。    

1.If we want to know more about Perl, we can type one of the following 3 commands:   

```perl 
perldoc perl  
perldoc perltoc  
perldoc perlintro  

```     
or you can just use the "man perl" command.  

2. More on perldoc  

```perl  
perldoc perlsyn  
#this will show the info of Perl syntax.   

perldoc perldata  
#this will show the info of Perl data types.  

perldoc perlop  
#this will show the info of Perl operators and precedence.


perldoc perlre   
#this will show the info of Perl regular expressions.   

perldoc perllol  
#this will show the info of Manipulating arrays of arrays in Perl.   

perldoc perlsub  
#this will show the info of Perl subroutines.    

perldoc perlfunc   
#this will show the info of Perl buintin functions.   

perldoc perlfaq  
#this will show the info of frequently asked questions about perl 
 
perldoc perlstyle
#this will show the info of Perl style guide.  

perldoc perltrap  
#this will show the info of Perl traps for the unwary. 

```  

3.If want to look for the info a funcion in perl, we can do:  

```perl  
perldoc -f split
#take split as an example.  
```  

For all those asked-often questions, you can use the following command to take a look at it:  

```perl  

perldoc -q sleep   

```    
4.聪明的人知道他们可以改变自己的态度， 信念和行为， 而且他们知道如何去改变。  
 
5.In emacs, we can use "M-X perldb" to enable the perl debugging mode.  







