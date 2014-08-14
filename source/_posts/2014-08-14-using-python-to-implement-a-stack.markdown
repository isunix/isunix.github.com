---
layout: post
title: "using python to implement a stack"
date: 2014-08-14 10:53:40 +0800
comments: true
categories: Algorithms
---
In this post, we are going to implement a stack using Python. We are gonna do it using two ways. The first is by pushing to the end of the list, and pop out the rightmost item. The second is by "pushing" to the leftmost and pop out the leftmost item.  

1. push to the end  

```py
class Stack:
    def __init__(self):
        self.items = []

    def is_empty(self):
        return self.items == []

    def push(self, item):
        self.items.append(item)

    def pop(self):
        return self.items.pop()

    '''
    returns the top item from the stack but does not remove it.
    It needs no parameters.
    The stack is not modified.
    '''
    def peek(self):
        return self.items[len(self.items) - 1]

    def size(self):
        return len(self.items)

s = Stack()
print (s.is_empty())
s.push(4)
s.push('dog')
print (s.peek())
print("\n")
print (s.peek())
s.push(True)
print (s.size())
print (s.is_empty())
s.push(8.4)
print (s.pop())
print (s.pop())
print (s.size())
```  

2. push to the front end

```py
class Stack:
    def __init__(self):
        self.items = []

    def is_empty(self):
        return self.items == []

    #push, inserting at the front end.
    def push(self, item):
        self.items.insert(0, item)

    #pop out the leftest item.
    def pop(self):
        return self.items.pop(0)

    def peek(self):
        return self.items[0]

    def size(self):
        return len(self.items)

s = Stack()
s.push('hello')
s.push('true')
print(s.pop())
print (s.pop())
```