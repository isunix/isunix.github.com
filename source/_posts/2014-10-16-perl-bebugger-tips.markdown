---
layout: post
title: "perl bebugger tips"
date: 2014-10-16 15:31:54 +0800
comments: true
categories: Perl
---
Knowing how to debug a perl program is really important. I am saying this not simply because it is supposed to be so, but also because I have encountered several occasions where I am stucked because I do not know how to debug and I have to ask for help from others. 

I am writing this post currently based on two perl pods, one is "perldebug", the other is "perldebtut". There is book named "perl debugged" which focuses on how to debug a perl program. Also google it to find post and materials as to how to debug a perl program. I am preparing to stuff all tips and knowledges regrading to perl debugging in this post.  

1.if we want to do a syntax check, we can use the following way:  

```pl
perl -c hello
```

2.The line shown is the one that is about to be executed next, it hasn't happened yet. So while we can print a variable with the letter 'p', at this point all we'd get is an empty (undefined) value back. What we need to do is to step through the next executable statement with an 's'. Then you can see the previous shown variable using the "p varname" format.  

3.type something like "x keys %data" will print out the data in a pretty format. 

```pl
Evals expr in list context, dumps the result or lists methods
```  

4.using the "x" operator on a hash is not quite useful here. since a couple of welcomes in there, but no indication of which are keys, and which are values, it's just a listed array dump and, in this case, not particularly helpful. The trick here, is to use a reference to the data structure:  

```pl
x \%data
```  

5.Know the differences between "qw" and "q": qw// is simply q// followed by a split on whitespace. No way to conserve blanks. Thus if the quoted words have blank spaces, and you want to treat them as a whole, use q rather than qw.  

5.perl -w script-name will execute the script and give out the warning messages.  

6.Take a closer look at the 'x' command, it's really useful and will merrily dump out nested references, complete objects, partial objects - just about whatever you throw at it.   

7.If we want to start the debugger and want some form of input from STDIN, we give it something non-committal, a zero: 

```pl
perl -de 0	
or 
perl -de0
```

8.typing "perl -de 0" into the terminal, build an on-the-fly object over a couple of lines (note the backslash):  

```pl
DB<1> $obj = bless({'unique_id'=>'123', 'attr'=> \
cont: 	{'col' => 'black', 'things' => [qw(this that etc)]}}, 'MY_class')
```

9.use the "x" command to see the internals of the obj. 

```pl
DB<2> x $obj
```

10.To give more examples on using the "perl -de 0" command, I will just copy the code from the "perldebtut" pod page.  

```pl
DB<3> @data = qw(this that the other atheism leather theory scythe)
DB<4> p 'saw -> '.($cnt += map { print "\t:\t$_\n" } grep(/the/, sort @data))
```

11.If you want to see the command History, type an 'H':

```pl
DB<5> H
```  

12.And if you want to repeat any previous command, use the exclamation: '!':  

```pl
DB<5> !4
```

13.If we want to put a breakpoint on a line, we can use this:  

```pl
b linenum
```   

14.We can see what breakpoints are set by using the list 'L' command:  

```pl
DB<3> L
```  

15.To delete a break point on a line, we use the "B" command. 

```pl
DB<3> B 16
```

16.At the end of the tutorial, its recommended to refer to the following tutorials:  

```
perldebug, perldebguts, perldiag, perlrun
```  

17.Option s and n does step by step execution of each statements. Option s steps into the subroutine. Option n executes the subroutine in a single step (stepping over it).

The s option does stepping into the subroutine while n option which would execute the subroutine(stepping over it).











	
