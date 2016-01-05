---
layout: post
title: ""spacemacs tips""
date: 2015-12-28 14:25:23 +0800
comments: true
categories: Emacs
---
1. comment out line/lines:

```html
Shift-V to select the line/lines to comment
Space-; to comment out the selected line/lines
```

2. switch to another buffer.

```
ctrl-x o
```

3. when we start emacs, we can press "q" to get rid of the welcome page.

4. We can use "ctrl-x ctrl-e" to execute a piece of code.

5. "ctrl-h v var" for more info on the variable, "ctrl-h f function" for more info on the function. "ctrl-h i m elisp" for more info on lisp, For spacemace, "space h i" for more info.

6. select some text, and "space-: indent-region" to indent the text you selected.

7. "M-x ielm" or "space-: ielm" will get you into the interactive elisp interface.

8. "ctrl-x b" to switch to a buffer.

9. For spacemacs, "SPC f e h" will give comprehensive documentation for each layer.

10. For spacemacs, go to the dir "~/.emacs.d/layers/+distribution/spacemacs/packages.el" for packages defaultly installed and enabled.

11. spacemacs quick guide:

```html
https://github.com/syl20bnr/spacemacs/blob/master/doc/QUICK_START.org
```

12. To open a dot file:

```
<SPC> f e d
```

13. to get the spacemacs version you are using:

```
SPC f e v
```

14. when we open a .py file, press "space + m" for more commands on short cuts. Like "space m s i" for "python-start-or-switch-repl"

15. For org-mode, press "shift+tab" to expand or fold the lists.