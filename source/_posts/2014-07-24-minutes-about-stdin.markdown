---
layout: post
title: "Perl中的stdin备忘"
date: 2014-07-24 17:26:27 +0800
comments: true
categories: Perl
---
There are some minute details about perl that we need to take care. So here I take a note for later reminder. 

1. STDERR will print out the error messages to the screen or to a file if you want.   

2. If we have a line of code like:  
 
  ```perl  
  $GetALine = <STDIN>;
  ```

It will wait for the user to enter something and then append a line ending character to the string that the user enters. 