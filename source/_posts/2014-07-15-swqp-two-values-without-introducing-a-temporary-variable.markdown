---
layout: post
title: "swap two values without introducing a temporary variable"
date: 2014-07-15 13:29:26 +0800
comments: true
categories: C
---

The usual way for us to swap two values in c is by introducing a intermediate variable. But actually there is way for us to complete the task wnile not adding a new varible.   

```c

#include <stdlib.h>
#include <stdio.h>

int main(){
  int a, b;
  scanf("%d %d", &a, &b);
  a = b - a;
  b = b - a;
  a = b + a;

  printf("%d %d\n", a, b);
  return 0;
}

```