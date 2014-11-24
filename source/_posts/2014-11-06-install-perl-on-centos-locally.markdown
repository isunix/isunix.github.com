---
layout: post
title: "install perl on centos locally"
date: 2014-11-06 16:55:54 +0800
comments: true
categories: Perl
---
Following the following steps to install perl in the local directory on your machine.

```pl
tar -xzf perl-5.10.1.tar.gz
cd perl-5.10.1
./Configure -des -Dprefix=$HOME/local
make
make test
make install
```