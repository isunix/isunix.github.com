---
layout: post
title: "static variable in c"
date: 2014-09-12 18:18:08 +0800
comments: true
categories: C
---
Static variables are the final type of variable available; these variables keep their value between calls to a function. About their effects, we will take a look at them through the following examples.

```c
#include <stdio.h>

int main(int argc, char *argv[]) {
    int i;

    for (i=1; i<=10; i++)
      printf("%d\n", i);

    return(0);
}
```

We all know it will print out 1, 2, till 10.  

If we change it a little bit, like thhis:  

```c
#include <stdio.h>

int foo (void) {
    int x = 0;
    return ++x;
}

int main(int argc, char *argv[]) {
    int i;

    for (i=1; i<=10; i++)
        printf("%d\n",foo());

    return(0);
}
```

This program will print out 1, all 1.  

What if we want to print out the "i" incrementally, we will use the static keyword.  

```c
#include <stdio.h>

int foo (void) {
    static int x = 0;
    return ++x;
}

int main(int argc, char *argv[]) {
    int i;

    for (i=1; i<=10; i++)
        printf("%d\n",foo());
    return(0);
}
```
This example is excerpted from the book "extending and embedding perl".  



