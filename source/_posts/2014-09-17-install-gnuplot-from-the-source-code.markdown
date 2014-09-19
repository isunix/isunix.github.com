---
layout: post
title: "install gnuplot from the source code"
date: 2014-09-17 10:38:15 +0800
comments: true
categories: Perl
---
On the centos server, I want to install gnuplot in my local dir, here are the steps:  

1. download the source code and cd into the dir.

2. ./configure --prefix=$HOME/local --with-readline=gnu

3. make

4. make install

That is all. 