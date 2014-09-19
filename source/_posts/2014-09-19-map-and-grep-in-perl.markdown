---
layout: post
title: "map and grep in perl"
date: 2014-09-19 12:27:58 +0800
comments: true
categories: Perl
---
I ran across some usage of grep and map in perl in some of the scripts I am reading. just to keep a note here. 

```pl
my @line = grep {not /^\s*$/} map {chomp;$_} <FILEIN>;  

@keyorder = grep {not /^\s*$/} @column;  

$rh_meta->{$meta_name} = {
	map {
		($_, 1)
	} grep {
		not /^\d+$/;
	} ($meta_body =~ /(\w+)/g)
	
$str =~ tr/a-z/A-Z/;
##how to use tr
```

I also come across some usage of redo and labeled loop, please see the following examples.

```pl
#!/usr/bin/perl
for $i (0..9) {
    for $j (0..9) {
        print "$i x $j\n";
        last if $i ==3;
    }
}
#the one without labeled loop, the "last" will only act on the inner loop.
```

if we want the "last" to act on the "outer" loop, we can do the following:  

```pl
#!/usr/bin/perl
LO: for $i (0..9) {
        for $j (0..9) {
            print "$i x $j\n";
            last LO if $i ==3;
        }
    }
```

namely we can use "labeled loop" to control the outer loop from the inner loop.

for the redo function, the difference it has to "next" is "next" will go to the next loop, while "redo" will just "redo" the current loop, this is partilarly useful if we want to ask the user to re-enter the password if they get the password wrong:  

```pl
use utf8;

my @words = qw{ fred barney pebbles dino };
my $errors = 0;

foreach (@words) {
    print "type the word '$_': ";
    chomp(my $try = <STDIN>);
    if ($try ne $_) {
      print "sorry, it is not right\n";
      $errors++;
      redo;
    }
}
##if you did not enter the right item, you will be asked and again!
```