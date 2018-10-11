---
layout: post
title: "common tips using java to practice algorithms"
date: 2014-08-14 10:07:16 +0800
comments: true
categories: Algorithms
---
There are common structues and tips while practicing algorithms and data structueres using java. I will try to keep them down in this post.   

1.hash tables  

```java
public HashMap<Integer, Student> buildMap(Student[] students) {
  HashMap<IntegerJ Student> map = new HashMap<Integer, Student>();
    for (Student s : students) map.put(s.getld(), s);
    return map;
}
``` 

2.ArrayList(Dinamically Resizing Array) 

```java
public ArrayList<String> merge(String[] words, String[] more) {
  ArrayList<String> sentence = new Arrayl_ist<String>();
  for (String w : words) sentence.add(w);
  for (String w : more) sentence.add(w);
  return sentence;
}
```   

3.StringBuffer   

```java
public String joinWords(String[] words){
  StringBuffer sentence = new StringBuffer();
  for (String w : words){
    sentence.append(w);
  }
  return sentence.toString();
}
```  

4.LinkedList  

```java  
class Node {
  Node next = null;
  int data;

  public Node(int d) {
  data = d;
  }

  void appendToTail(int d) {
    Node end = new Node(d);
    Node n = this;
    while (n.next != null) {
      n = n.next;
    }
    n.next = end;
  }
}
```  

5.Deleting a node from a singly linkes list.  

```java
Node deleteNode(Node head, int d) {
  Node n = head;

  if (n.data == d) {
    return head.next; /* moved head */
  }

  while (n.next 1= null) {
    if (n.next.data == d) {
      n.next = n.next.next;
      return head; /* head didn't change */
    }
    n = n.next;
  }
  return head;
}
```  

6.Implementing a stack

```java
class Stack {
  Node top;

  Object pop() {
    if(top != null) {
      Object item = top.data;
      p = top.next;
      return item;
    }
    return null;
  }

  void push(0bject item) {
    Node t = new Node(item);
    next = top;
    top = t;
  }

  Object peek() {
    return top.data;
  }
}
```  

7.Implementing a queue.  

```java  
class Queue {
  Node first, last;

  void enqueue(0bject item) {
    if(first == null) {
      last = new Node(item);
      first = last;
      } else {
        last.next = new Node(item);
        last = last.next;
      }
  }

  Object dequeueQ {
    if (first != null) {
      Object item = first.data;
      first = first.next;
      return item;
    }
    return null;
  }
}
```

8.pseudocode to implement DFS

```java
void search(Node root) {
  if (root == null) return;
  visit(root);
  root.visited = true;
  foreach (Node n in root.adjacent) {
    if (n.visited == false) {
      search(n);
    }
  }
}
```  

9.BFS.

```java
void search(Node root) {
  Queue queue = new QueueQ;
  root.visited = true;
  visit(root);
  queue.enqueue(root); // Add to end of queue

  while (!queue.isEmpty()) {
    Node r = queue.dequeueQ; // Remove from front of queue
    foreach (Node n in r.adjacent) {
      if (n.visited == false) {
        visit(n);
        n.visited = true;
        queue.enqueue(n);
      }
    }
  }
}
```
