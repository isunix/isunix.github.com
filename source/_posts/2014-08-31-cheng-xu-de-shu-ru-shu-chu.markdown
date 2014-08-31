---
layout: post
title: "程序的输入输出"
date: 2014-08-31 10:45:18 +0800
comments: true
categories: C
---
介绍三种程序的输入输出方法。   


```c
#include <stdlib.h>
#include <stdio.h>
#define INF 100000

int main(){

  int x, n=0, min=INF, max=-INF, s=0;
  while(scanf("%d", &x) == 1){
    s += x;
    if (x < min) min=x;
    if (x > max) max=x;
    n++;
  }
  printf("%d %d %.3f\n", min, max, (double)s/n);
  return 0;
}
```    

```c
#define LOCAL
#include <stdlib.h>
#include <stdio.h>
#define INF 10000000

int main(){
  #ifdef LOCAL
    freopen("data.in", "r", stdin);
    freopen("data.out", "w", stdout);
  #endif

  int x, n=0, min=INF, max=-INF, s=0;
  while(scanf("%d", &x) == 1){
    s += x;
    if (x < min) min=x;
    if (x > max) max=x;
    n++;
  }
  printf("%d %d %.3f\n", min, max, (double)s/n);
  return 0;
}
```   

```c
#include <stdlib.h>
#include <stdio.h>
#define INF 10000000

int main(){
  FILE *fin, *fout;
  fin = fopen("data.in", "rb");
  fout = fopen("data.out", "wb");


  int x, n=0, min=INF, max=-INF, s=0;
  while(fscanf(fin, "%d", &x) == 1){
    s += x;
    if (x < min) min=x;
    if (x > max) max=x;
    n++;
  }

  fprintf(fout, "%d %d %.3f\n", min, max, (double)s/n);
  fclose(fin);
  fclose(fout);
  return 0;
}
```

