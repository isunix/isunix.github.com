---
layout: post
title: "polymorphism in perl"
date: 2014-09-10 14:37:37 +0800
comments: true
categories: Perl
---
This is mainly a note from the book "object oriented perl programming" by Damian Conway.


When a method is called on a particular object, the actual method that’s involved may depend on the class to which the object belongs. For instance, if we call an object’s ignite() method, its response will be different depending on whether it belongs to the Paper, Rocket, Passion, or FlameWar class.    

1.inheritance polymorphism:

the objects whose methods are called belong to a hierarchy of classes that are related by inheritance. The presence of the required method in the base class of the hierarchy ensures that objects of any derived class can always respond, if only generically, to a given method call. The ability to re- define individual methods in derived classes allows objects of those classes to respond more spe- cifically to a particular method call if they so wish.    

2.interface polymorphism:  

The alternative approach to polymorphism is to allow any object with a suitable method to respond to a call to that method. This is known as interface polymorphism, because the only requirement is that a particular object’s interface provides a method of the appropriate name. Consequently, languages that allow interface polymorphism must also provide a run-time mechanism for handling cases where an object is unable to provide a requested method. Typ- ically, this involves providing a means of specifying a fallback subroutine that is called when- ever an object cannot respond to a particular method invocation. Alternatively, such languages may have some form of exception system. In that case, the language will trigger a well-defined exception if the object cannot respond more appropriately.Inheritance polymorphism is a special case of interface polymorphism because a common base class guarantees that objects share a specific inherited method. Any language that supports interface polymorphism automatically supports inheritance polymorphism as well.

3.abstract class:   

A class hierarchy will contain some classes—typically near the top of the hierarchy—that were never intended to be used to build objects directly. In other words, these classes exist only to represent a shared category or provide a single source from which descendent classes can inherit shared methods. Such classes are called abstract base classes. There is one additional role that an abstract base class can fulfill. Any base class, abstract or not, can be used to ensure that every class derived from it has a specific polymorphic method. That’s a handy feature because we are then guaranteed that any derived class will be able to respond polymorphically to a specified set of method calls.    

Abstract base classes are clearly useful, but in large object-oriented systems two problems can arise. The first is that they may accidentally be used as real classes when someone mistakenly creates an object of their type.   

Although an abstract base class ensures that a derived class has a certain set of methods, it does not require that the derived class redefine any of those methods meaningfully. This can be a problem if many such polymorphic methods are inher- ited, and we accidentally forget to redefine one of them. The result is that a particular class uses the generic behavior for a polymorphic function, instead of its own appropriate class-specific behavior.  

Many object-oriented programming languages solve these two problems by introducing the concept of an abstract method (which is also known as a pure virtual function, or a deferred feature). An abstract method is a method in an abstract base class that has no valid implementation and exists only to indicate a necessary part of each derived class’s interface. It is a kind of placeholder in the interface, indicating the need for a certain functionality, but not actually providing it.     

Suppose, for example, the register() method of the Truck class had been declared as an abstract method (i.e., defined but not implemented). Now, because that ancestral regis- ter() method doesn’t provide a working implementation, whenever a Truck object is creat- ed, and its register() method is called, an error will be flagged. This immediately solves the general problem of incorrect use of objects belonging to an abstract base class.  
Better still, it also solves the problem of forgetting to redefine a method in a derived class. For example, if the person coding the FireTruck class neglects to implement a suitable reg- istration method for that class, then the register() method inherited from Truck will be called instead. Rather than performing some inadequate default registration process, the in- herited abstract method will immediately signal an error, indicating that the implementation is incorrect.

4.Objects can live beyond the program that creates them.   

5.Object-oriented programming languages provide an important separa- tion between how data is used externally—the methods that can be called on an object—and how that data is represented and manipulated internally—the way its attribute values are stored, and its methods are coded. So long as the interface remains stable, the implementation can be changed as necessary—optimized, extended, parallelized, distributed, and so forth.   

6.In object-oriented terms, persistence is the ability of objects to retain their attribute values, their association with a class, and their individual identity, between separate executions of a program. In other words, persistent objects are those that, next time you start running the program, are still there.   

Persistence requires more than just dumping an object’s attribute values into a file or a database when the program terminates, and then creating a new object, and reloading the saved data next time the program executes. The essence of persistence is that when the program next executes, a persistent object will have been identifiably reconstructed, either with the same name, the same location in memory, or another way of accessing it that is consistent between executions.    

Moreover, the reconstruction ought to be as fully automated as possible. Ideally, the pro- grammer should only have to somehow mark an object as persistent, and thereafter it will au- tomagically reappear every time the program executes. In practice, very few languages can achieve that level of transparency.    

More often, to create a persistent object it is necessary to create a special-purpose class, perhaps by deriving it from the object’s original class. This, in turn, requires the programmer to create some custom code to translate internal representations of the object—the bit patterns representing it in the program—to external representations—the bit patterns in a file or database.   

This translation process is called encoding or serialization and is difficult to implement in the general case. It’s particularly hard if some attributes of a persistent object store pointers or references to other data. In such cases, it may also be necessary to also encode the data being referred to, as well as the abstract relationship between the persistent objects involved. In an inherently persistent language, this requirement must be met for an arbitrary number of at- tributes storing arbitrary interrelationships between arbitrary objects of arbitrary classes. Not surprisingly, few languages fully support both object orientation and automatic persistence.     

Another important issue is the granularity of the persistence conferred upon objects. Some languages, such as HyperTalk, offer fine-grained persistence, in which every change in the attributes of an object is immediately recorded externally. Most, however, offer only coarse- grained persistence, where the attributes of an object are recorded only at the very end of a pro- gram’s execution.   

Coarse-grained persistence is almost always a more efficient alternative since it minimizes the amount of disk access a program performs. Fine-grained persistence, on the other hand, is clearly the safer alternative since it ensures that an object’s state can always be reconstructed in a subsequent execution of the program, even if a previous execution terminated prematurely.    

Of course, in practice, not even the finest of fine-grained persistence offers any real guar- antee of data integrity. Even if an object is updated every time it is modified, the program might still crash in the middle of the update process itself, or, in crashing at some other point, it might somehow trash the file system on which the object was recorded. However, these prob- lems also apply to coarse-grained persistence, which is far more likely to lose data due to an inopportune termination since, in general, nothing at all will have been recorded prior to the crash.   

6.In the literature on object-oriented programming, standard concepts pass by many strange aliases. It some- times seems that every object-oriented language designer deliberately invents a completely new set of names for the same fundamental ideas.

(I strong agree with Dimian Conway, many concepts are so clear to clear to understand, yet people invent new new aliases to mask the concept thus makes other people hard to digest the essence under those concepts--by Steven)   
