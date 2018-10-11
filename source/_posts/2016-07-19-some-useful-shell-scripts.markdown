---
layout: post
title: "some useful shell scripts"
date: 2016-07-19 09:31:05 +0800
comments: true
categories: Shell
---
Here is a collection of those *sh commands I used that I think might be useful for later usage.

1.compare two directories and see if the differences between them.

```sh
diff -urNa test test1
```

2.find all files with "old" in their filename, and then romove them

```sh
find ./ -name "*old*" -exec rm -i {} \;
```

3.grep

```sh
ll | grep "Jul 20" | awk '{print $NF}' | xargs -I , grep -i "Successfully" , | wc -l
```

4.substitute string in multiple files and backup the orignal files with "~"

```sh
find . | xargs grep "good" -sl | uniq | xargs perl -pi~ -e 's/good/bad/g'
```

5.substitute string in multiple files and backup the orignal files with extension "bak"

```sh
find . | xargs grep "bad" -sl | uniq | xargs perl -i.bak -p -e 's/bad/excellent/g'
```

After checking that everything is ok, we can then remove those "bak" files

```sh
find ./ -name "*bak*" -exec rm -i {} \;
```

6.grep lines before and aftern certain matching line

```sh
grep -C 4 '. $kpi_shell $load_date' orig_cron_kpi.sh  | grep "\.sh" | less
```

7.grep lines in one file while not in the other.

```sh
grep -F -x -v -f bb.txt aa.txt | grep "\.sh" | less
```