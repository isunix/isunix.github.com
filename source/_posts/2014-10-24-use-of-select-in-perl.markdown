---
layout: post
title: "Perl中的select的使用"
date: 2014-10-24 13:34:51 +0800
comments: true
categories: Perl		
---
One of the best illustration of the use of select I read maybe from the book "data munging with perl".   

Look at the the differences between the following 3 ones.  

```pl
print;    
print LIST;
print FILEHANDLE LIST;
```
 
For the first one "print", since on target is specified, the contents of ```$_``` are printed to the default output file handle(usually STDOUT).    

For the second one "print LIST", the contents of LIST are printed to the default output file handle.  

For the third one "print FILEHANDLE LIST", the contents of LIST are printed to the specified file handle, "FILEHANDLE".  

If you call select with no parameters, it will return the name of the currently selected output file handle, so 

```pl
print select; 
```  
will normally print main::STDOUT.   

If you call select with the name of a file handle, it will replace the current default output file handle with the new one. It returns the previously selected file handle so that you can store it and reset it later. If you
need to write a lot of data to a particular file, you could use code like this:   

```pl
open FILE, '>out.txt' or die "Can't open out.txt: $!";
my $old = select FILE;
foreach (@data) {
	print;
}
select $old;
```    

Another variable that is useful when writing data is ```$|```. Setting this variable to a nonzero value will force the output buffer to be flushed immediately after every print (or write) statement. This has the effect of making the output stream look as if it were unbuffered. This variable acts on the currently selected output file handle. If you want to unbuffer any other file handle, you will need to select it, change the value of ```$|```, and then reselect the previous file handle using code like this:   

```pl
my $file = select FILE;
$| = 1;
select $file;
```  

In its compact form, it can be written as:  

```pl
select((select(FILE), $| = 1)[0]);
```   

Finally we will take a look at an example,  

```pl
open(FILE,">./test.out");
$oldHandle = select(FILE);
print select;
print "This is sent to test.out.\n";
$second = select($oldHandle);
print "to default stdout!\n";
print $second;
```  

If you understand how "select" works, the output for this piece of code is quite obvious.  