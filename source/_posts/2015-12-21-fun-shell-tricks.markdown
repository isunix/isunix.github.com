---
layout: post
title: "fun shell tricks"
date: 2015-12-21 15:04:39 +0800
comments: true
categories: Shell	
---
1.Print the 10 most frequent words in the input.

```sh
cat * | tr -sc A-Za-z '\n' | sort | uniq -c | sort -n | tail
```

Sadly this is not totally correct, it will give out something like:

```
22 pl
38 d
```

which are not exactly words.

2.use awk with substr:

```sh
date | awk '{print substr($4, 1, 5)}'
```