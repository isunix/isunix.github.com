---
layout: post
title: "php-cgi not found error"
date: 2014-06-07 14:56:33 +0800
comments: true
categories: PHP
---
Today while I was running a php script from the PHPStrom by a browser, I got the following error telling me that "php-cgi not found.". I have no other way but to install a new version of php, my original version is 5.4.24, I then installed a 5.5 version.  

```bash
curl -s http://php-osx.liip.ch/install.sh | bash -s 5.5
```

and in my phpstorm, I use the path, "usr/local/php5/bin" as the interpreter's path. It works now.

