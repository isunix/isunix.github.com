---
layout: post
title: "some useful linux commands"
date: 2014-12-18 12:33:58 +0800
comments: true
categories:
---
I will keep notes of some of the useful Linux commands here.  

1.say you want to find something, we can use the "find" command or the convenient "ack" script.

```sh
find . -iname "*stsun*" -delete
```

This will find all files containing 'stsun' and then execute the delete command.

2.awk '{print $2 $1}' text.txt

3.tr '[A-Z]' '[a-z]' < test.txt

4.sed '125!d' text.txt

5.awk 'NR==125' text.txt

6.to print out the shebang, do the following:

```pl
 my $interpretr = $ENV{_};
 print $interpreter;
```
It will print out the interpreter that runs the script.

7.to cat a file and open it to a filehandle, 

```pl
open (FH, "cat $file |") or die "can't open the given file";
```

Pay attention to the "|" here, because in normal file opening, it is not needed.




