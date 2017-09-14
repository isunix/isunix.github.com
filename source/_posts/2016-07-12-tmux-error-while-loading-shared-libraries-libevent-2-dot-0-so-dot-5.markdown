---
layout: post
title: "tmux: error while loading shared libraries: libevent-2.0.so.5"
date: 2016-07-12 10:34:50 +0800
comments: true
categories: Shell
---
I have kept a blog on tmux installation which is about missing module libevent, and the post is on:

```html
http://isunix.github.io/blog/2014/12/24/libevent-not-found-error-while-install-tmux/
```

Recently even after I install the livevent module, I still get the following errors after installing tmux and then running tmux:

```
 ./tmux: error while loading shared libraries: libevent-2.0.so.5: cannot open shared object file: No such file or 
```

I installed the libevent lib in $HOME/local/lib, and tmux says it can not find the library, Weird. With the help of one of my colleague, this problem is solved.

```sh
export DIR="$HOME/local"
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$DIR/lib
./configure --prefix=$DIR CFLAGS="-I$DIR/include" LDFLAGS="-L$DIR/lib"
make
make install
```

As we can see, the point here is setting the "LD_LIBRARY_PATH" variable.