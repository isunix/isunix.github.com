---
layout: post
title: "basics of linux screen"
date: 2016-05-26 14:52:24 +0800
comments: true
categories: Linux
---
A basic of introduction of linux screen.

1.To create a new screen session without the name specified, just type 

```sh
screen
``` 

2.To create a new screen session with the name specified, just type

```sh
screen -S sessionname
```

3.To detach from a session, type “Ctrl-A” and “d“

4.To list all the sessions , type "screen -ls"

5.To re-attach to a session, type "screen -r sessionname"

6.To switch between windows, type "Ctrl-A" then then enter the window number. Or just "Ctrl-A" followed by pressing "p" or "n".

7.Type “Ctrl-A” and “?” without quotes. Then you will see all commands or parameters on screen.

8.Type “Ctrl-A” and “:” without quotes, then enter "sessionname NAME" to rename an existing sessioin.