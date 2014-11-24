---
layout: post
title: "notes on shell scripts"
date: 2014-11-10 16:40:55 +0800
comments: true
categories: Shell
---
While reading some of the scripts written by my colleagus, I found some usages to be quite tricky. Thus I keep a note of the usage here.


1.filename and extension parts

```sh
echo `basename $PWD` # Basename of current working directory.echo "${PWD##*/}" # Basename of current working directory.echoecho `basename $0` # Name of script.echo $0 # Name of script.echo "${0##*/}" # Name of script.echofilename=test.dataecho "${filename##*.}" # data# Extension of filename.
```  

2.