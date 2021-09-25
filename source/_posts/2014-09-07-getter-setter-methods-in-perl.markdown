---
layout: post
title: "Perl中的getter-setter方法"
date: 2014-09-07 12:49:26 +0800
comments: true
categories: Perl
---
As well as getting the value of an attribute, you may well want to set or change it. The syntax you’ll use is as follows:   

```pl
print "Old address: ", $object->address(), "\n";
$object->address("Campus Mirabilis, Pisa, Italy");
print "New address: ", $object->address(), "\n";
```  

This kind of accessor is called a get-set method because you can use it to both get and set the attribute. Turning your current read–only accessors into accessors that can also set the value is simple. Let’s create a get–set method for address():   

```pl  

sub address {
	my $self = shift;
	# Receive more data
	my $data = shift;   

	# Set the address if there's any data there.
	$self->{address} = $data if defined $data;
	return $self->{address};

}
```  

If you don’t particularly want to trap calling the method as a class method (since it’ll generate an error when we try to access the hash entry anyway), you can write really miniature get–set methods like the following:   

```pl
sub address { $_[0]->{address } = $_[1] if defined $_[1]; $_[0]->{address } }    

sub lastname { $_[0]->{lastname } = $_[1] if defined $_[1]; $_[0]->{lastname } }    

sub firstname { $_[0]->{firstname} = $_[1] if defined $_[1]; $_[0]->{firstname} }
```

