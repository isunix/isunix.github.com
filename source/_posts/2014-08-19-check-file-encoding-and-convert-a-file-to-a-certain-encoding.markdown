---
layout: post
title: "check file encoding and convert a file to a certain encoding"
date: 2014-08-19 13:58:55 +0800
comments: true
categories: Python
---
The case scenario is: I have namy source files of codes and the commoents there and some print messages are in English, of course I can open the file in vim and issue the following command to make them to utf-8 encoding:  

```vim
:set fileencoding=utf8
```   
The question here is I have many files thus I do not want to do this repeatedly. So a script to ease the pain is needed.   

If we want to know the file's encoding, we can issue the following command:  

```pl
file filename  
or
file -mime filename  
```

Ok, I am stucked here, I have no idea how to do this ritht now. mabe later.   



