---
layout: post
title: "object oriented perl chap02"
date: 2014-10-28 14:08:34 +0800
comments: true
categories: Perl
---
This is a note about chap02 in "Object oriented perl".  

1.For a hash, we have two ways to get the key-value pair.  

```pl
my %hash = (
    steven => "good",
    sun    => "bad",
);

my $nextkey;

while (defined($nextkey = each %hash)){
    print "the key $nextkey has the value $hash{$nextkey}\n";
}
```   

The other way is:  

```pl
my %hash = (
    steven => "good",
    sun    => "bad",
);

while (($nextkey, $nextval) = each %hash){
    print "the key $nextkey has value $nextval\n";
}
```   

2.Subroutines can also be declared with a prototype, which is a series of specifiers that tells the compiler to restrict the type and number of arguments with which the subroutine may be invoked. For example, in the subroutine definition:  

```pl
sub insensitive_less_than ($$) {	return lc($_[0]) lt lc($_[1]);}
```  

The prototype is ```($$)``` and specifies that the subroutine insensitive_less_than can only be called with exactly two arguments, each of which will be treated as a scalar—even if it’s actually an array!  

Prototypes are only enforced when a subroutine is called using the name(args) syntax. Prototypes are not enforced when a subroutine is called with a leading & or through a subroutine reference.   

3.Here is a clear illustration of how to use reference in Perl:  

```pl
my @row1 = (1, 2, 3);
my @row2 = (4, 5, 6);
my @row3 = (7, 8, 9);

my @cols = (\@row1, \@row2, \@row3);
my $table = \@cols;

print "2 x 3 is ", $table->[1]->[2];
```  

4.Here is a script to realize the function of skipping along an array by a fixed step size. It uses anynymous soubroutine and closure.  

```pl
sub hop_along{
    my ($from, $to, $step) = @_;
    my $next = $from - $step;
    my $closure_ref = sub{
        $next += $step;
        return if $next > $to;
        $_[0] = $next;
        return 1;
    };
    return $closure_ref;
}

$iterator = hop_along(1, 100, 7);
while($iterator->($next)){
    print $next." ";
}
``` 

The sad thing is, I am not sure if this is the best way to achieve the function.
