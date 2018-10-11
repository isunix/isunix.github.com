---
layout: post
title: "minutes on setting up emacs on macos"
date: 2015-07-02 15:29:18 +0800
comments: true
categories: Linux
---
1. I am am using gui emacs and I want to it to be started from the command line, then I have to do this:

```sh
alias emacs='open -a /Applications/Emacs.app $1'
```

2. I want to change the default font and font size:

```sh
(set-default-font "Monaco 28")
```

3. I want to use evil, after putting it into ~/.emacs.d, also I need to put the folliwng things in to ~/.emacs.d/init.el

```
(add-to-list 'load-path "~/.emacs.d/evil")
(require 'evil)
(evil-mode 1)
```

4. I am using slime, so I have to put the following things into my ~/.emacs.d/init.el

```
(setq inferior-lisp-program "/usr/local/bin/sbcl")
(setq slime-contribs '(slime-fancy))
```