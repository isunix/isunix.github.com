---
layout: post
title: "object oriented perl chap03"
date: 2014-10-28 16:58:25 +0800
comments: true
categories: Perl
---
This is a note about chap03 in “Object oriented perl”.  

1.In object oriented perl, there are three rules,

```pl
1. rule1: To create a class, build a package.   
2. rule2: To create a method, write a subroutine.
3. rule3: To create an object, bless a referent.
```    

2.Some cases while calling a method through an arrow:  

```pl
$hsh_ref->{"key"};# Access the hash referred to by $hashref$arr_ref->[$index];# Access the array referred to by $arrayref$sub_ref->(@args);# Access the sub referred to by $subref$obj_ref->method(@args);# Access the object referred to by $objref
```  

3.When a method like ```Bug::print_me``` is called, the argument list that it receives begins with the object reference through which it was called, followed by any arguments that were explicitly given to the method. That means that calling 

```pl
Bug::print_me("logfile")
``` 

is not the same as calling 

```pl
$nextbug->print_me("logfile")
```

In the first case, print_me is treated as a regular subroutine so the argument list passed to ```Bug::print_me``` is equivalent to:

```pl
( "logfile" )
```
In the second case, ```print_me``` is treated as a method so the argument list is equivalent to:   

```pl
( $objref, "logfile" )
``` 

Having a reference to the object passed as the first parameter is vital, because it means that the method then has access to the object on which it’s supposed to operate. Hence you’ll find that most methods in Perl start with something equivalent to this:   

```pl
package Bug;
sub print_me{
	my ($self) = shift;
}
```  

or better still:  

```pl
package Bug;
sub print_me{
	my ($self, @args) = @_;
}
```  
This second version is better because it provides a lexically scoped copy of the argument list ```(@args)```.   

4.Unlike other object-oriented languages, Perl doesn’t require that an object be a special kind of recordlike data structure. In fact, you can use any existing type of Perl variable—a scalar, an array, a hash—as an object in Perl.   

5.The ```bless``` function takes two arguments: a reference to the variable to be marked and a string containing the name of the class. It then sets an internal flag on the variable, indicating that it now belongs to the class.  

6.We didn’t bless the reference; we blessed the referent. The scalar didn’t change—only the nameless hash it refers to has been marked.   

7.You can check that the blessing succeeded by applying the built-in ref function to ```$nextbug```. Normally, when ```ref``` is applied to a reference, it returns the type of that reference.  

```pl
my $nextbug = {
    _id => "00001",
    _type => "fatal",
    _descr => "application does not compile"
};
bless $nextbug, "Bug";
print ref($nextbug);
```

THe above code gives out the result, ```Bug```.   

8.Based on the things we said above, we will show a piece of code to demonstrate how to get and set attributes in perl.

```pl
package CD::Music;
use strict;

{
    my $_count = 0;
    sub get_count{$_count}
    sub _incr_count{++$_count}
}

sub new {
    my ($class, @arg) = @_;
    $class->_incr_count();
    bless{
        name => $_[1],
        singer => $_[2],
        album => $_[3],
        rating => $_[4],
    }, $class;
}

sub name{ $_[0] -> {name} }
sub singer{ $_[0] -> {singer} }
sub album{ $_[0] -> {album} }

sub rating {
    my ($self, $rating) = @_;
    $self -> {rating} = $rating if $rating;
}

package main;

my $cd = CD::Music->new("谁的眼泪在飞", "孟庭苇", "谁的眼泪在飞", 7);

print $cd->name, "\n";

print $cd->singer."\n";

print $cd->album, "\n";

print $cd->rating(8)."\n";

print "There have been ", CD::Music->get_count(), " CD[s] created\n";
```
