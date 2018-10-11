---
layout: post
title: "useful shell commands"
date: 2016-05-30 16:13:41 +0800
comments: true
categories: Shell
---
1.In bash shell, it provides us with two options to make debugging very much easier. "-v" and "-x".

Take the following small script for an example.

```sh
#!/bin/bash
echo "You are using $0"
echo "Hello $*"
exit 0
```

If run with the follwoing "-v" option, 

```sh
bash -v aa.sh steven
```

We will get the following result,

```
#!/bin/bash
echo "You are using $0"
You are using aa.sh
echo "Hello $*"
Hello steven
exit 0
```

If run with the "-x" option, we will get the following result.

```
+ echo 'You are using aa.sh'
You are using aa.sh
+ echo 'Hello steven'
Hello steven
+ exit 0
```

As we can see, "-x" might be more helpful to us.


2.We can use "read -p" to read from the user input and store the input into an variable. Like this:

```sh
read -p "Enter your name: " name
echo $name
exit 0
```

3.use the "-s" option with "read" to control the visibility of the entered text.

```sh
#!/bin/bashread -p "May I ask your name: " nameecho "Hello $name"read -sn1 -p "Press any key to exit"echoexit 0
```

4.Grep with "-c" option to list the number of items grepped.