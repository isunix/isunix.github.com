---
layout: post
title: "cgi set up on macos"
date: 2014-09-30 16:57:08 +0800
comments: true
categories: Perl
---
There are multiple guidelines as to how to set up cgi for perl on macos or linux. 

This post keeps notes of how to set up cgi on MACOS.

```pl
ln -s /Library/WebServer/CGI-Executables ~/www/cgi-bin
cd ~/www/cgi-bin
```
put scripts in this dir and access it using the link "localhost/cgi-bin/filename" 

you may need to change the permission of the script to "755" if needed.

