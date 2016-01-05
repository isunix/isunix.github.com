---
layout: post
title: "from bash to zshell"
date: 2016-01-05 11:39:52 +0800
comments: true
categories: Shell
---
Some useful shell commands gathered here.

1. Nested for loop:

```sh
for dir in `echo "$PATH" | tr ':' ' '`docd "$dir"  for file in *  do    ...test each $file in this $dir and    output its name if it's a program...  donedone | sort > proglist```

2. Just learned that "ctrl-z" will terminate a process, then we can use "fg" command to restart the process.

3. To restart a stopped job and put it into the background, use the shell’s bg command; the arguments are job numbers. We can use the "jobs" command to show the jobs.

4. For zsh,

```
Esc-p Go to the previous line starting with the same word
Esc-n Go to the next line starting with the same word
Ctrl-k Kill to the end of line
Ctry-y Yank the last killed text
```

5. We can use the "run-help" command to find the help page for commands, like

```sh
run-help set
```
