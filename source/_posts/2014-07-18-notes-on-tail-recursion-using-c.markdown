---
layout: post
title: "C语言里面的尾递归的例子"
date: 2014-07-18 13:50:41 +0800
comments: true
categories: C
---
还是先上一段递归的c代码吧:  

```c
#include <stdlib.h>
#include <stdio.h>

int FibonacciRecursive(int n){
  if(n < 2){
    return n;
  }
  return (FibonacciRecursive(n-1) + FibonacciRecursive(n-2));
}

int main(){
  printf("Fibonacci number till 6 is: %d\n", FibonacciRecursive(6));
}

```    

而所谓的尾递归就是把当前的运算结果（或路径）放在参数里传给下层函数, 采用尾递归的算法示例如下:   

```c

int FibonacciTailRecursive(int n, int ret1, int ret2){
  if(n==0){
    return ret1;
  }
  return FibonacciTailRecursive(n-1, ret2, ret1 + ret2);
}

```   

一下是一个在别人的博客中看到的利用递归还有尾递归来求单链表的长度的例子。 

```c
#include <stdlib.h>
#include <stdio.h>

typedef struct node{
  int data;
  struct node* next;
}node, *linklist;

void InitLinklist(linklist* head){
  if(*head != NULL){
    free(*head);
  }
  *head = (node*)malloc(sizeof(node));
  (*head)->next = NULL;
}

void InsertNode(linklist* head, int d){
  node* newNode = (node*)malloc(sizeof(node));
  newNode->data = d;
  newNode->next = (*head)->next;
  (*head)->next = newNode;
}

//using recursion to get the length of the linklist;
int GetLengthRecursive(linklist head){
  if(head->next == NULL){
    return 0;
  }
  return (GetLengthRecursive(head->next) + 1);
}

//using tail recursive to get the length of a linklist,
//with the help of the variable "acc" to store the length of the current linklist, increment it

int GetLengthTailRecursive(linklist head, int *acc){
  if(head->next == NULL){
    return *acc;
  }
  *acc = *acc + 1;
  return GetLengthTailRecursive(head->next, acc);
}

void PrintLinklist(linklist head){
  node* pnode = head->next;
  while(pnode){
    printf("%d->", pnode->data);
    pnode = pnode->next;
  }
  printf("->NULL\n");
}

int main(){
  linklist head = NULL;
  int len = 0;
  InitLinklist(&head);
  InsertNode(&head, 10);
  InsertNode(&head, 21);
  InsertNode(&head, 14);
  InsertNode(&head, 19);
  InsertNode(&head, 132);
  InsertNode(&head, 192);
  PrintLinklist(head);
  printf("The length of linklist is: %d\n", GetLengthRecursive(head));
  GetLengthTailRecursive(head, &len);
  printf("the length of linklist is: %d\n", len);
}

```