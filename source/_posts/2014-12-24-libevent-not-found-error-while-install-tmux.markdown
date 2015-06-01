---
layout: post
title: "libevent not found error while install tmux"
date: 2014-12-24 21:13:11 +0800
comments: true
categories: Shell
---
While I was installing tmux on cent-os, I met the error saying that "libevent not found", something like this. Then I download libevent and install it into the location '/home/stsun/local' dir.

Still I get the error saying that "libevent not found". I solved the problem by the following way.

```sh
DIR="$HOME/local"
./configure --prefix=$DIR CFLAGS="-I$DIR/include" LDFLAGS="-L$DIR/lib"
```

Since I install libevent with the option, "--prefix=$HOME/local".