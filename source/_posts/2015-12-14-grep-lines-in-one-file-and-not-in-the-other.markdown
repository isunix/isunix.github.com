---
layout: post
title: "grep lines in one file and not in the other"
date: 2015-12-14 14:46:10 +0800
comments: true
categories: Shell
---
Say we have a file a, which has the following contentL:

```
a
b
c
d
e
```

and b,

```
c
d
```

What if we want to get all those in file a and not in file b, in this case, a, b, e?

```sh
grep -F -x -v -f b.txt a.txt
```

To qutoe from the page

```html
http://unix.stackexchange.com/questions/28158/is-there-a-tool-to-get-the-lines-in-one-file-that-are-not-in-another
```

The above command is doing the following things:

```
This works by using each line in b.txt as a pattern (-f b.txt) and treating it as a plain string to match (not a regular regex) (-F). You force the match to happen on the whole line (-x) and print out only the lines that don't match (-v). Therefore you are printing out the lines in a.txt that don't contain the same data as any line in b.txt.
```

So remember the order of file a and b matters if you really understand what the command is doing.
