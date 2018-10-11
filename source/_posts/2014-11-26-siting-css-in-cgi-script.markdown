---
layout: post
title: "siting css in cgi script"
date: 2014-11-26 17:09:55 +0800
comments: true
categories: Perl
---
While writing perl cgi scripts, when we need to add css or js files, there are two ways to add the file, one using absolute path, one using relative path. 

First we want to check the document root of our file, we cat get it using the following way. 

```pl
#!/usr/bin/env perl

print "Content-type: text/plain; charset=utf-8\n\n";
print $ENV{DOCUMENT_ROOT};
```

For example, in my case, it gives out the following result:  

```pl
"/usr/local/www/apache22/data"
```

We assume that our server name is gopid.com, in the /usr/local/www/apache22/ dir, there are the data dir, cgi-bin dir, we make a sub-dir named steven in the data dir, then we can using the following two ways to site the css and js files.

```html
<link type="text/css" href="/steven/js/bootstrap/css/bootstrap.min.css" rel="stylesheet">
<link type="text/css" href="/steven/css/margin.css" rel="stylesheet">
```

Or using the absolute path: 

```html
<link type="text/css" href="https://goopig.com/steven/js/bootstrap/css/bootstrap.min.css" rel="stylesheet">
<link type="text/css" href="https://goopig.com/steven/css/margin.css" rel="stylesheet">
```

PS, if we want to print out the whole env infomation using cgi, we can using the following script:  

```pl
#!/usr/local/bin/perl

print "Content-type: text/plain; charset=utf-8\n\n";
foreach $var (sort(keys(%ENV))) {
    $val = $ENV{$var};
    $val =~ s|\n|\\n|g;
    $val =~ s|"|\\"|g;
    print "${var}=\"${val}\"\n";
}
```


