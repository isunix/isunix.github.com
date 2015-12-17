---
layout: post
title: "useful bash scripts"
date: 2015-09-10 11:31:53 +0800
comments: true
categories: Shell
---
This post keeps notes of some useful bash scripts or one liners.

1.find files with txt ext in the current dir and print out those files to be deleted and then delete those files.

```sh
find . -type f -name "*.txt" -print |xargs -I {} sh -c "echo deleting {}; rm {}"
```

2.find files with txt ext in the current dir and mv those files to another dir with amount of files limited to a certain number:

```sh
find ./ -type f -name "*.txt"| xargs -L56 -I {} mv -f {} ./old/
```

3.Almost same with step 2, but also print out the steps taken in the command line:

```sh
find ./ -type f -name "*.txt"| xargs -L56 -I {} -t mv {} ./old/
```

4.find if a dir is a subdir of another dir:

```sh
dir_a="/home/stsun"
dir_b="/home/stsun/work/spam"

if [[ "${dir_b}" == "${dir_a}"* ]]
then
    # Get the subdirectory only
    SUBDIR=${dir_b#${dir_a}/}
    printf "SUBDIR is $SUBDIR\n"
    BASE=${dir_a}/${SUBDIR%%/*}
    printf "BASE is ${BASE}\n"

else
    printf "Error: ${dir_b} is not in ${dir_a}\n"
    exit 1
fi
```

