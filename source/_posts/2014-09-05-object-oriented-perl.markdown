---
layout: post
title: "object oriented perl"
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