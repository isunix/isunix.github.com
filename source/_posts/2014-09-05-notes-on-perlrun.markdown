---
layout: post
title: "notes on perlrun"
date: 2014-09-05 19:24:02 +0800
comments: true
categories: Perl
---
We keep notes on some of the useful notes on perl command line knowledge here.  

1.-i[extension]:  

specifies that files processed by the "<>" construct are to be edited in-place.  It does this by renaming the input file, opening the output file by the original name, and selecting that output file as the default for print() statements.   

2.-p:
causes Perl to assume the following loop around your program, which makes it iterate over filename arguments somewhat like sed.