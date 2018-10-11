---
layout: post
title: "链表的两种实现方式"
date: 2014-08-02 10:31:18 +0800
comments: true
categories: Algorithms
---
这是关于线性表链式存住的两种实现方式，一个使用指针，一个使用c++中的引用。其实这两种方式是大同小异的。  

The first method will use pointer in c.  

```c  
/*first inlcude all those need header files.*/
#include "stdio.h"
#include "string.h"
#include "ctype.h"
#include "stdlib.h"
#include "math.h"

/*define those constants needed*/
#define OK 1
#define ERROR 0
#define TRUE 1
#define FALSE 0

/*define the initial size allocated.*/
#define MAXSIZE 20

/*define the return type of a function*/
typedef int Status;
typedef int ElemType;

/*define a struct Node with the name Node, and make LinkList a pointer point to Node*/
typedef struct Node {
    ElemType data;
    struct Node *next;
}Node;
typedef struct Node *LinkList;

/*initialize the LinkList*/
Status InitList(LinkList *L)
{
    *L=(LinkList)malloc(sizeof(Node));     
    if(!(*L)) 
    	return ERROR;
    (*L)->next=NULL; 

    return OK;
}

Status ListEmpty(LinkList L){
    if(L->next)
    	return FALSE;
    else
    	return TRUE;
}

/*if the linklist already exists, set it to empty*/
Status ClearList(LinkList *L)
{
	LinkList p,q;
	p=(*L)->next;     /*p points to the first node*/      
	while(p)          /*it means not to the end of the linklist*/      
	{
		q=p->next;
		free(p);
		p=q;
	}
	(*L)->next=NULL;  /*pointer field for the head Node will be null*/       
	return OK;
}

/*return the length of the linklist*/
int ListLength(LinkList L)
{
    int i=0;
    LinkList p=L->next;  /*p points to the first node*/
    while(p)
    {
        i++;
        p=p->next;
    }
    return i;
}

/*get the i th element of L and returning its value using e*/
Status GetElem(LinkList L,int i,ElemType *e) {
	int j;
	LinkList p;		/* declare a node "p" */
	p = L->next;		/* let p point to the first node of L */
	j = 1;		
	while (p && j<i)  
	{
		p = p->next;  /* let p point to the next node */
		++j;
	}
	if ( !p || j>i )
		return ERROR;  /*  the i th element does not exist */
	*e = p->data;   /*  get the data of the i th element */
	return OK;
}

/* locate element e in L */  
int LocateElem(LinkList L,ElemType e) {
    int i=0;
    LinkList p=L->next;
    while(p)
    {
        i++;
        if(p->data==e) /* find the element */
                return i;
        p=p->next;
    }

    return 0;
}
	
/*insert at the location of the i th element*/ 	
Status ListInsert(LinkList *L,int i,ElemType e)
{
	int j;
	LinkList p,s;
	p = *L;
	j = 1;
	while (p && j < i)     /* find the i th node */
	{
		p = p->next;
		++j;
	}
	if (!p || j > i)
		return ERROR;   
	s = (LinkList)malloc(sizeof(Node));  
	s->data = e;
	s->next = p->next;      
	p->next = s;          
	return OK;
}  

/*delete the i th element, returning its value using e*/

Status ListDelete(LinkList *L,int i,ElemType *e)
{
	int j;
	LinkList p,q;
	p = *L;
	j = 1;
	while (p->next && j < i)	
	{
        p = p->next;
        ++j;
	}
	if (!(p->next) || j > i)
	    return ERROR;           
	q = p->next;
	p->next = q->next;			
	*e = q->data;               
	free(q);                   
	return OK;
}

/*print out all elements*/  

Status visit(ElemType c) {
    printf("%d ",c);
    return OK;
}

Status ListTraverse(LinkList L)
{
    LinkList p=L->next;
    while(p)
    {
        visit(p->data);
        p=p->next;
    }
    printf("\n");
    return OK;
}

/*create the data for the n elements randomly, create a linked list with head node*/

void CreateListHead(LinkList *L, int n)
{
	LinkList p;
	int i;
	srand(time(0));                         
	*L = (LinkList)malloc(sizeof(Node));
	(*L)->next = NULL;                      
	for (i=0; i<n; i++)
	{
		p = (LinkList)malloc(sizeof(Node)); 
		p->data = rand()%100+1;             
		p->next = (*L)->next;
		(*L)->next = p;						
	}
}

/*create the data for the n elements randomly, create a linked list with tail node*/

void CreateListTail(LinkList *L, int n)
{
	LinkList p,r;
	int i;
	srand(time(0));                      
	*L = (LinkList)malloc(sizeof(Node)); 
	r=*L;                                
	for (i=0; i<n; i++)
	{
		p = (Node *)malloc(sizeof(Node)); 
		p->data = rand()%100+1;           
		r->next=p;                        
		r = p;                            
	}
	r->next = NULL;                       
}

/*in the main function you  have to do the following initializations*/ 

int main()
{
    LinkList L;
    ElemType e;
    Status i;
    int j,k;
    i=InitList(&L);
	/*blahblah*/
}

```  

The following is a version using c++'s reference "&", it is a little different, but mostly wil be the same as the above.  

```cpp
#include <stdio.h>
#include <stdlib.h>

typedef char ElemType;
typedef struct LNode  		
{
	ElemType data;
	struct LNode *next;		
} LinkList;

/*creating the linked list by inserting at the head*/  

void CreateListF(LinkList *&L,ElemType a[],int n)
{
	LinkList *s;int i;
	L=(LinkList *)malloc(sizeof(LinkList));  	
	L->next=NULL;
	for (i=0;i<n;i++)
	{
		s=(LinkList *)malloc(sizeof(LinkList));
		s->data=a[i];
		s->next=L->next;			
		L->next=s;
	}
}

/*creating the linked list by inserting at the tail*/
void CreateListR(LinkList *&L,ElemType a[],int n)
{
	LinkList *s,*r;int i;
	L=(LinkList *)malloc(sizeof(LinkList));  	
	L->next=NULL;
	r=L;					
	for (i=0;i<n;i++)
	{
		s=(LinkList *)malloc(sizeof(LinkList));
		s->data=a[i];
		r->next=s;			
		r=s;
	}
	r->next=NULL;			
}

/*and blah and blah*/

```