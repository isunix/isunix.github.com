---
layout: post
title: "线性表顺序存储的的指针实现以及引用实现"
date: 2014-08-01 12:23:17 +0800
comments: true
categories: Algorithms
---
在线性表的顺序存储中， 我们既可以使用指针来实现这些抽象的数据类型，也可以使用C++中的引用来操作。   

下面让我们来先用指针来实现。   

For the sake of convenience, the following paragraphs will be using English to illustrate now.  

```c
#include "stdio.h"    
#include "stdlib.h"   
#include "math.h"    

#define OK 1
#define ERROR 0
#define TRUE 1
#define FALSE 0
/*In c, there there is no "TRUE" or "FALSE"*/   

#define MAXSIZE 20
typedef int Status;
typedef int ElemType; 

/*define a struct*/
typedef struct {
	ElemType data[MAXSIZE];        
	int length;                                
}SqList;  

/*initial the sequential list, as we can, L is a pointer*/    
Status InitList(SqList *L) { 
    L->length=0;
    return OK;
}

/*test if the initial sequential list is empty, not here the argument "L" is not a pointer*/
Status ListEmpty(SqList L) { 
	if(L.length==0)
		return TRUE;
	else
		return FALSE;
}  

/*if not empty, clean it*/
Status ClearList(SqList *L) { 
    L->length=0;
    return OK;
}

/*if alreay exists, return its length*/ 
int ListLength(SqList L) {
	return L.length;
}

/*get the i th element, return its value using e*/ 
Status GetElem(SqList L,int i,ElemType *e) {
    if(L.length==0 || i<1 || i>L.length)
            return ERROR;
    *e=L.data[i-1];

    return OK;
}

/*find the element e*/
int LocateElem(SqList L,ElemType e) {
    int i;
    if (L.length==0)
            return 0;
    for(i=0;i<L.length;i++)
    {
            if (L.data[i]==e)
                    break;
    }
    if(i>=L.length)
            return 0;

    return i+1;
}  

/*if L already exists, insert element e in front of element i, add the length of L by 1*/
Status ListInsert(SqList *L,int i,ElemType e)
{ 
	int k;
	if (L->length==MAXSIZE)  
		return ERROR;
	if (i<1 || i>L->length+1)
		return ERROR;

	if (i<=L->length) {
		for(k=L->length-1;k>=i-1;k--)  
			L->data[k+1]=L->data[k];
	}
	
	L->data[i-1]=e;          
	L->length++;

	return OK;
}  

/*delete the i th element of L, returing its value using e, subtract the length by 1*/  
Status ListDelete(SqList *L,int i,ElemType *e) 
{ 
    int k;
    if (L->length==0)               
		return ERROR;
    if (i<1 || i>L->length)         
        return ERROR;
        
    *e=L->data[i-1];
    
    if (i<L->length) {
        for(k=i;k<L->length;k++)
			L->data[k-1]=L->data[k];
    }
    
    L->length--;
    return OK;
}

/*print out an element in L*/
Status visit(ElemType c) {
    printf("%d ",c);
    return OK;
}

/*if L already exists, using the visit function defined above to traverse L and print out the whole List*/  
Status ListTraverse(SqList L){
	int i;
    for(i=0;i<L.length;i++)
            visit(L.data[i]);
    printf("\n");
    return OK;
}

/*After all these steps above, now we will define our "main" function. */

int main() {
	SqList L;
	ElemType e;
	Status i;
	/*and blabla*/
}
 
```  

We will then realize the  "reference" version using c++.  

First we will create a file named "sqlist.cpp".  

```cpp
#include <stdio.h>
#include <stdlib.h>
#define MaxSize 50

typedef char ElemType; 
typedef struct {
	ElemType data[MaxSize];		
   	int length;					
} SqList;  

/*create the list*/  
void CreateList(SqList *&L,ElemType a[],int n) {
	int i;
	L=(SqList *)malloc(sizeof(SqList));
	for (i=0;i<n;i++)
		L->data[i]=a[i];
	L->length=n;
}

/*initial the list*/  
void InitList(SqList *&L) {
	L=(SqList *)malloc(sizeof(SqList));	
	L->length=0;
}

/*destroy the list*/  
void DestroyList(SqList *&L) {
	free(L);
}

/*test if the list is empty or not*/
int ListEmpty(SqList *L)
{
	return(L->length==0);
}

/*return the list's length if it exists*/  
int ListLength(SqList *L) {
	return(L->length);
}   

/*show the list, same as the "traverse" function above*/  
void DispList(SqList *L) {
	int i;
	if (ListEmpty(L)) return;
	for (i=0;i<L->length;i++)
		printf("%c ",L->data[i]);
	printf("\n");
}  

/*get the i th element of L, returning its value using e*/  
int GetElem(SqList *L,int i,ElemType &e) {
	if (i<1 || i>L->length)
		return 0;
	e=L->data[i-1];
	return 1;
}

/*find the element e in L*/  
int LocateElem(SqList *L, ElemType e) {
	int i=0;
	while (i<L->length && L->data[i]!=e) i++;
	if (i>=L->length)
		return 0;
	else
		return i+1;
}

/*insert element e infront of i in L, right shift the element after data[i]*/
int ListInsert(SqList *&L,int i,ElemType e) {
	int j;
	if (i<1 || i>L->length+1)
		return 0;
	i--;						
	for (j=L->length;j>i;j--) 	
		L->data[j]=L->data[j-1];
	L->data[i]=e;
	L->length++;				
	
	return 1;
}  

/*delete element i in L, returning its value using e*/ 
int ListDelete(SqList *&L,int i,ElemType &e){
	int j;
	if (i<1 || i>L->length)
		return 0;
	i--;						
	e=L->data[i];
	for (j=i;j<L->length-1;j++)	
		L->data[j]=L->data[j+1];
	L->length--;				
	return 1;
}

```  

We can just "#include "sqlist.h"" in a file where we want to use all those function defined in sqlist.h