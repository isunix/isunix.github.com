---
layout: post
title: "p4 add new executable script"
date: 2015-12-02 13:38:57 +0800
comments: true
categories: linux
---
This post shows how to add a script into p4 repo.

```sh
p4 add cross-rules-freqs.pl
p4 edit -t text+x cross-rules-freqs.pl
p4 submit
```