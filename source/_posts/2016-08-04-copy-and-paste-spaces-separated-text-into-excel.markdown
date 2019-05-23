---
layout: post
title: "copy and paste spaces separated text into excel"
date: 2016-08-04 16:06:03 +0800
comments: true
categories: Linux&Mac
---
最近经常需要把空格作为delimiter的文本粘贴到excel里。之前的做法是

```sh
cat aa.log | awk '{print $1}' | pbcopy
```
来一列一列地copy到excel里。甚是繁琐。 excel不会用的啊。

今天发现了原来还可以这么来操作。

1. 把整个文件的内容粘贴到excel里去
2. 在excel中选中文件内容， 然后点击 Data->Text to Columns, 然后选择合适的delimiter去把文本内容给搞到excel中去。

Bingo！
