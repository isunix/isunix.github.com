---
layout: post
title: "update all perl modules through cpanm"
date: 2016-03-31 16:54:00 +0800
comments: true
categories: Perl
---
I want to update all the installed Perl modules using cpanm. Here is a method I found.

```sh
cpan-outdated -p | cpanm
```

We have to first download the module "http://search.cpan.org/CPAN/authors/id/T/TO/TOKUHIROM/App-cpanoutdated-0.24.tar.gz" and then issue the command to update the modules.
