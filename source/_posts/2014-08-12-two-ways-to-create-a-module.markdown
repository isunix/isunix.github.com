---
layout: post
title: "Perl中创建module"
date: 2014-08-12 20:51:22 +0800
comments: true
categories: Perl
---
There are two build systems for building a module. One is to use the old and stable "ExtUtils::Makemaker", and new one is using "Module::Build". We will use the Module::Starter module to help us create a module.  

By default, Module::Starter create a distribution with Makefile.PL

First with Makefile.PL  

```pl
module-starter --module="Animal" --author="Steven Sun" --email=steven.sun2013@gmail.com --verbose    

This is the same as:  
module-starter --builder="ExtUtils::Makemaker" --module="Animal" --author="Steven Sun" --email=steven.sun2013@gmail.com --verbose    

perl Makefile.PL   
make
make test   
make disttest  
make dist
```

Next we will show you the "Build.PL"

```pl  
module-starter --builder="Module::Build" --module="Animal" --author="Steven Sun" --email=steven.sun2013@gmail.com --verbose 

or in a simpler way, we can do this:  
module-starter --mb --module="Animal" --author="Steven Sun" --email=steven.sun2013@gmail.com --verbose  

perl Build.PL   
./Build  
./Build test
./Build disttest       ##this will create a .tar.gz archive which we can distribute now.  
./Build dist
```

For the Module::Build way, there is a shortcut.   

We don’t want to type that long command line every time, so module-starter can get that information from a      
configuration file $HOME/.module-starter/config. If we’re on Windows, that .module-starter name is a bit of a      
problem, so we can set the MODULE_STARTER_DIR environment variable to the name of the directory that contains
config. Inside config, we can list the parameter names and values separated by a colon.

```perl

author: Steven Sun  
email: steven.sun2013@gmail.com  
builder: Module::Build  
verbose: 1
```  
Once we have our configuration file setup, life is much easier since we only need to specify the name of the distribution that we want to create. 

```perl  

% module−starter −−module=Animal  
```
