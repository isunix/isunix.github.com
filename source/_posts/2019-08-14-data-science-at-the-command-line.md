---
layout: post
title: "Data Science at the Command Line"
date: 2019-08-14 14:13:16 +0800
comments: true
categories: Data&ML&AI
---

本文是关于如何使用命令行的方式，来更好的认识你的数据.

## 1. 常用的命令和工具:

- 基本操作命令

  ```shell
  cd, mv, cat, ls, wc, rm, sort, uniq, echo
  printf, pwd, mkdir, dirname, mktemp， find
  mail, sendmail, crontab, export, ps
  zip, du, df, tar, split
  exec, type, readlink
  ```

- 基本工具

  ```shell
  grep, egrep, pcregrep, ack
  curl, wget
  ssh, tmux
  awk, sed
  ```

- 辅助命令

  ```shell
  jq, git,
  man, tldr
  conda, pip
  ```

- 辅助工具

  ```shell
  zsh, oh-my-zsh, sexy-bash-prompt
  ```

-  瑞士军刀

  ```shell
  Perl
  ```



## 2. 一些应用场景:

- 使用 `split` 按照特定的行数或者大小，将一个文本进行分割

  ```shell
  # Split a file, each split having 10 lines (except the last split)
  split -l 10 filename
  # plit a file with 512 bytes in each split
  split -b 512 filename
  ```

- 使用 `grep -x -f`  找到两个文件中的相同的行

  ```shell
  grep -x -f  file1 file2
  ```

- 使用 `grep` 或者 `egrep` 或者 `pcregrep` 或者 `ack` 并且辅助以正则表达式， 进行复杂的文本搜索

  ```shell
  # print file name with the corresponding line number for each match
  grep -Hn search_string path/to/file
  # invert match for excluding specific strings:
  grep -v search_string path/to/file
  # search in case-insensitive mode:
  grep -i search_string path/to/file
  # search consecutive 9 numbers
  grep -E '\d{9}' path/to/file
  # search consecutive 9 numbers and grab it
  grep -Eo '\d{9}' path/to/file
  # recursively search
  grep -eilr "\bamazfit\b\|\bwatch\b" path/to/dir
  ```

- `ssh` 登陆远程机器并且同时运行远程操作命令

  ```shell
  # ssh 远程执行命令
  ssh yyy@xxx.xxx.xxx.xxx "df -h"
  # ssh 使用key文件登陆， 并且做远程的端口转发
  ssh -L 9007:${hive_server} ${xiaomi_host} -N -i ${keyfile}
  ```

- `awk` 按照特定的分隔符，查看文本有多少列， 查看想要看的列，按照条件进行筛选

  ```shell
  # 以空格做分隔符， 并且打印出第二列小于20的行
  awk '($2 < 20){print}'
  # 以'#' 做分隔符， 并且打印出第二列小于20的行
  awk -F '#' '($2>=8){print}'
  # 以',' 做分隔符， 并且打印出列数
  awk -F"," '{print NF}'
  # 有多个判断条件
  awk '{if ($4<1 && $4>=0.85 && $2 >= 0.001) print $7}'
  ```

- `sort` 结合 `uniq` 去重

  ```shell
  du -cks * | sort | uniq | wc -l
  ```

- `xargs` 传递参数

  ```shell
  # xargs 结合 kill 来干掉进程
  ps auxww | grep file | grep -v grep | awk '{print $2}' | xargs kill -9
  # 删除找到的文件
  find . -name "*.txt" | xargs -I , rm -rf ,
  ```

- 使用 `jq` 命令来在命令行下更好的查看json文件

  ```shell
  cat file.json | jq
  ```

- 非常好用的 `|`

  ```shell
  xx | yy | zz | dd | ee | ff | gg | hh
  ```



## 3. 参考资料:

- [Linux 菜鸟教程](https://www.runoob.com/linux/linux-tutorial.html)

- [正则表达式 - 教程](https://www.runoob.com/regexp/regexp-tutorial.html)

- [Awesome-Shell](https://github.com/alebcay/awesome-shell)

参考链接:

- [csvkit](https://csvkit.readthedocs.io/en/latest/tutorial/1_getting_started.html#installing-csvkit)

- [Data Science at the Command Line]([https://www.datascienceatthecommandline.com](https://www.datascienceatthecommandline.com/))

