---
layout: post
title: "python linked list example"
date: 2015-07-27 16:21:27 +0800
comments: true
categories: Python
---
Will use python linked list to solve the following problem:


```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

    def __str__(self):
        return str(self.value)

class LinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    def addNode(self, value):
        node = Node(value)
        if self.head == None:
            self.head = node
            self.tail = node
        else:
            self.tail.next = node
            self.tail = node

    def __str__(self):
        if self.head != None:
            index = self.head
            nodeStore = [str(index.value)]
            while index.next != None:
                index = index.next
                nodeStore.append(str(index.value))
            return "LinkedList  [ " + "->".join(nodeStore) + " ]"
        return "LinkedList  []"

def generatedLinkedList(numArray):
    linkedlist = LinkedList()
    for i in range(len(numArray)):
        linkedlist.addNode(numArray[i])
    return linkedlist

```

Then we will start to solve the problem:

```python
from LinkedList import *

class ListsSum:
    def addLists(self, l1, l2):
        p1 = l1.head
        p2 = l2.head
        carry = 0
        linkedlist_sum = LinkedList()
        while (p1 != None) or (p2 != None) or (carry != 0):
            dig_sum = carry
            if p1 != None:
                dig_sum += p1.value
                p1 = p1.next
            if p2 != None:
                dig_sum += p2.value
                p2 = p2.next

            linkedlist_sum.addNode(dig_sum%10)
            carry = dig_sum/10
        return linkedlist_sum

if __name__ == '__main__':
    solution = ListsSum()
    list1 = generatedLinkedList([2,4,3])
    list2 = generatedLinkedList([5,6,4])
    print(list1)
    print(list2)
    print(solution.addLists(list1,list2))

```