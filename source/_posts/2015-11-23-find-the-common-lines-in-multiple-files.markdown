---
layout: post
title: "Linux命令从多个文件中找到公共的行"
date: 2015-11-23 17:22:11 +0800
comments: true
categories: Linux&Mac
---
What if I want to find the lines exist in all the given files under linux. Of course I can write a small script but I do not want to do that, cause I am sure there are commands for this kind of task.

```sh
grep -F -x -f file1 file2 ...
```

you can refer to the following page for more details.

```html
http://unix.stackexchange.com/questions/28158/is-there-a-tool-to-get-the-lines-in-one-file-that-are-not-in-another
```
