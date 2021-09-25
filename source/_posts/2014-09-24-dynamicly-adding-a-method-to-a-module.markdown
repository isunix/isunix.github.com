---
layout: post
title: "Perl中动态地往模块里添加module"
date: 2014-09-24 12:57:20 +0800
comments: true
categories: Perl
---
We can follow the following steps to add/change a method in a module dynamicly.  

```pl
use strict;
use warnings;
use utf8;
{

    package Data::Dumper;

    sub test {
        print "test to add a new method to Data::Dumper\n";
    }
}

use Data::Dumper;
Data::Dumper::test;
print Dumper \%Data::Dumper::
```

we can also use the following one liner to check the methods defined in a module:  

```pl
perl -e "use File::Find; use Data::Dumper; print Dumper \%File::Find::"  
```  

or we can use JSON to print out its format:  

```pl
perl -e "use File::Find; use JSON; print to_json(\%File::Find::)"  
```