---
layout: post
title: "how to make zsh the default shell without root access"
date: 2014-12-24 19:01:06 +0800
comments: true
categories: Shell
---
As depicted by the title, this post keeps notes on how to make zsh the default shell without root access. BTW, I am using oh-my-zsh configuration files.

In the .bash_profile, add the following lines,

```sh
export SHELL=/bin/zsh
exec /bin/zsh -l
```

Where zsh will be your own location of your zsh file.