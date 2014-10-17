---
layout: post
title: "bash script to list all methods in a perl module"
date: 2014-09-25 16:21:52 +0800
comments: true
categories: Shell 
---
In the post "Dynamicly Adding a Method to a Module", I showed how to use a perl one-liner to list all the methods in a module.  

I will show how to do it in a shell script thus we can accept the module on the command line, 

```sh
#!/bin/bash
perl -e "use Data::Dumper; use $1; print Dumper \%$1::"
```

