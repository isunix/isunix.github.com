---
layout: post
title: "kill a tmux window"
date: 2015-06-08 12:54:07 +0800
comments: true
categories: Perl
---
When we are using tmux and stuck there, we can then follow the following steps to kill the window.

```bash
tmux list-windows
tmux kill-window -t $window_number
```

