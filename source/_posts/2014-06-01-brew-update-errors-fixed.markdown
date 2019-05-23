---
layout: post
title: "brew update errors fixed"
date: 2014-06-01 16:12:00 +0800
comments: true
categories: Linux&Mac
---
I met several errors while updating my homebrew, one is:

{% img /images/sun/first.png %}

the solution is:

```
cd `brew --prefix`
git remote add origin https://github.com/mxcl/homebrew.git
git fetch origin
git reset --hard origin/master

```

the other is:

{% img /images/sun/second.png %}

To address this this error, we just have have to change the permissions on the folder to a certain user:

```
chown -R sun .git
```
