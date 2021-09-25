---
layout: post
title: "Perl一行命令删除空行"
date: 2014-07-24 15:05:16 +0800
comments: true
categories: Perl
---
Here below is the one-liner I found to remove a blank line in a file.   

```perl  

perl -pi -e 's!^\s+?$!!' file.txt  

```