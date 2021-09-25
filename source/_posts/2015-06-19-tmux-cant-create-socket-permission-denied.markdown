---
layout: post
title: "Tmux中的can't create socket: Permission denied问题解决"
date: 2015-06-19 13:04:00 +0800
comments: true
categories: Linux&Mac
---

my tmux's sockets are output to the dir "~/tmp", however today I encountered the problem saying "can't create socket: Permission denied" while I start tmux.

The reason is I have changed the rights on the folder ~/tmp/tmux* , so after the following command:

```sh
chmod 700 -R tmux*
```

It is back to normal.
