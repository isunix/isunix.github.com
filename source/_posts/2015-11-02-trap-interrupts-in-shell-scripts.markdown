---
layout: post
title: "Shell中的trap中断(interrupts)"
date: 2015-11-02 14:45:18 +0800
comments: true
categories: Shell
---
Today I met some shell scirpts like the following:

```sh
trap "rm -f $file; exit" INT TERM EXIT
```
More code here:

```sh
cleanup() {
    echo "Cleaning stuff up..."
    exit
}

trap cleanup INT TERM
echo ' --- press ENTER to close --- '
read var
cleanup
```

change "trap cleanup INT TERM" above to "trap cleanup INT TERM EXIT" and then execute the script. Enter 'exit' and see what differences will happen.

The following are references:

```html
http://unix.stackexchange.com/questions/57940/trap-int-term-exit-really-necessary
http://kb.mit.edu/confluence/pages/viewpage.action?pageId=3907156
```
