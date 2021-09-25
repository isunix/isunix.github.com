---
layout: post
title: "Perl面向对象"
date: 2014-09-05 15:46:51 +0800
comments: true
categories: Perl
---  

We can find details about the info list below by issuing "perldoc perlobj", or "perldoc perlootut"


1.When we bless something, we are not blessing the variable which contains a reference to that thing, nor are we blessing the reference that the variable stores; we are blessing the thing that the variable refers to (sometimes known as the referent).  

```pl

use Scalar::Util 'blessed';
my $foo = {};
my $bar = $foo;

bless $foo, 'Class';
print blessed( $bar );

$bar = "some other value";
print blessed( $bar );

```

The first will print out "Class" and second undef(of course you can see it).

When we call "bless" on a variable, we are actually blessing the underlying data structure that the variable refers to. We are not blessing the reference itself, nor the variable that contains that reference. That's why the second call to "blessed( $bar )" returns false. At that point $bar is no longer storing a reference to an
object. You will sometimes see older books or documentation mention "blessing a reference" or describe an object as a "blessed reference", but this is incorrect. It isn't the reference that is blessed as an object; it's the thing the reference refers to (i.e. the referent).   

2.Objects are merely Perl data structures (hashes, arrays, scalars, filehandles, etc.) that have been explicitly associated with a particular class. That explicit association is created by the built-in "bless" function.

3.An object is simply a data structure that knows to which class it belongs.A class is simply a package. A class provides methods that expect to operate on objects. A method is simply a subroutine that expects a reference to an object (or a package name, for class methods) as the first argument. 

4.Each package contains a special array called @ISA. The @ISA array contains a list of that class's parent classes, if any. This array is examined when Perl does method resolution. It is possible to manually set @ISA. and you may see this in older Perl code. Much older code also uses the base pragma. For new code, we recommend that you use the parent pragma to declare your parents.  This pragma will take care of setting @ISA.  It will also load the parent classes and make sure that the package doesn't inherit from itself.  

5.However the parent classes are set, the package's @ISA variable will contain a list of those parents. This is simply a list of scalars, each of which is a string that corresponds to a package name.   

6.All classes inherit from the UNIVERSAL class implicitly. The UNIVERSAL class is implemented by the Perl core, and provides several default methods, such as "isa()", "can()", and "VERSION()".  The "UNIVERSAL" class will never appear in a package's @ISA variable.  

7.Perl provides no special constructor syntax. This means that a class must implement its own constructor. A constructor is simply a class method that returns a reference to a new object.    

8.A simple read-only accessor simply gets the value of a single attribute:  

```pl

sub path {
	my $self = shift;
	return $self->{path};
} 
```  

A read-write accessor will allow the caller to set the value as well as get it:  

```pl

sub path {
	my $self = shift;

    if (@_) {
    	$self->{path} = shift;
    }

    return $self->{path};
}
```  

9.More on bless. 

```pl
my $object = bless {}, $class;
my $object = bless {};
```

In the first form, the anonymous hash is being blessed into the class
in $class. In the second form, the anonymous hash is blessed into the
current package. The second form is strongly discouraged, because it breaks the ability of a subclass to reuse the parent's constructor, but you may still run across it in existing code.   

10.If you simply want to check that a variable contains an object reference, we recommend that you use "defined blessed($object)", since "ref" returns true values for all references, not just objects.  

11.If you call a method that doesn't exist in a class, Perl will throw an error. However, if that class or any of its parent classes defines an "AUTOLOAD" method, that "AUTOLOAD" method is called instead.   

12.All the examples so far have shown objects based on a blessed hash. However, it's possible to bless any type of data structure or referent, including scalars, globs, and subroutines. You may see this sort of thing when looking at code in the wild.  

13.You should also check out perlmodlib for some style guides on constructing both modules and classes.  

14.As we said earlier, most Perl objects are hashes, but an object can be an instance of any Perl data type (scalar, array, etc.). Turning a plain data structure into an object is done by blessing that data structure using Perl's "bless" function.  

15.Once a referent has been blessed, the "blessed" function from the Scalar::Util core module can tell us its class name. This subroutine returns an object's class when passed an object, and false otherwise.  

16.A constructor creates a new object. In Perl, a class's constructor is just another method, unlike some other languages, which provide syntax for constructors. Most Perl classes use "new" as the name for their constructor: my $file = File->new(...);   

17.What makes a method special is how it's called. The arrow operator ("->") tells Perl that we are calling a method.   

18.When we make a method call, Perl arranges for the method's invocant to be passed as the first argument. Invocant is a fancy name for the thing on the left side of the arrow. The invocant can either be a class name
or an object. We can also pass additional arguments to the method:

```pl
sub print_info {
	my $self   = shift;
    my $prefix = shift // "This file is at ";

   	print $prefix, ", ", $self->path, "\n";
}

$file->print_info("The file is located at ");
# The file is located at /etc/hostname
```  

19.Each class can define its attributes. Attributes are sometimes called properties.  

20.Perl has no special syntax for attributes. Under the hood, attributes are often stored as keys in the object's underlying hash, but don't worry about this.   

21.You might also see the terms getter and setter. These are two types of accessors. A getter gets the attribute's value, while a setter sets it. Another term for a setter is mutator. We recommend that you only access attributes via accessor methods.   

22.Attributes are typically defined as read-only or read-write. Read-only attributes can only be set when the object is first created, while read-write attributes can be altered at any time.  

23.We often refer to inheritance relationships as parent-child or "superclass/subclass" relationships. Sometimes we say that the child has an is-a relationship with its parent class.   

24.The process of determining what method should be used is called method resolution. What Perl does is look at the object's class first ("File::MP3" in this case). If that class defines the method, then that class's version of the method is called. If not, Perl looks at each parent class in turn. For "File::MP3", its only parent is "File". If "File::MP3" does not define the method, but "File" does, then Perl calls the method in "File".  

25.It is possible to explicitly call a parent method from a child:

```pl
package File::MP3;

use parent 'File';  

sub print_info {
	my $self = shift;
	$self->SUPER::print_info();
	print "Its title is ", $self->title, "\n";
}

```  

26.The "has()" subroutine declares an attribute, and "Moose" automatically creates accessors for these attributes. It also takes care of creating a "new()" method for you. This constructor knows about the attributes you declared.     

27.与@INC数组类似，@INC包含文件的寻找路径, @ISA数组含有类(包)名，当一个方法在当前包中未找到的时就到@ISA中中的包去寻找。@ISA中还含有当前类继承的基类名。  

28.oo中的new可以有如下的几种写法的: 注意这两种写法的区别  

```pl
#!/usr/bin/perl
use Cocoa;
$cup = new Cocoa;
$cup->setImports( 'java.io.InputStream', 'java.net.*');
$cup->declareMain( "Msg" , "java.applet.Applet", "Runnable");
$cup->closeMain();  

or 

#!/usr/bin/perl
use Cocoa;
$cup = new Cocoa;
Cocoa::setImports($cup, 'java.io.InputStream', 'java.net.*');
Cocoa::declareMain($cup, "Msg" , "java.applet.Applet", "Runnable");
Cocoa::closeMain($cup); 

```    

29.类方法通过@ISA数组继承.


