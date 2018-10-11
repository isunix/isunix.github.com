---
layout: post
title: "login to mysql server without entering password"
date: 2015-06-01 10:58:02 +0800
comments: true
categories: Perl
---
Enter the user name and password in a shell script in the following way will make the login process easier.

```bash
mysql -h $host -u$user -p$pass $db
```
