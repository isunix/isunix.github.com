---
layout: post
title: "remove the ^M chareacters in a file"
date: 2014-07-01 13:45:23 +0800
comments: true
categories: Vim
---
In a file that have multiple "^M" characters in it , we can use vim to remove them.

```perl

:%s/^M//g

```

the ^M character is made by typing ctrl + v first then hit enter.


Also I write a perl script to convert the from dos to unix and also delete chars in code followng the "//".

```perl

open($IN, "$ARGV[0]") or die "in: $@";
open($OUT, ">", "$ARGV[0].new") or die "out: $@";

while (<$IN>){
    my $line = $_;
    $line =~ s/(\/\/.*)//g;
    print $OUT $line;
}

$command = "mv $ARGV[0].new $ARGV[0] && chmod 777 $ARGV[0] && dos2unix $ARGV[0]";

system($command);
print "successfully deleted and converted!\n";
close($IN);
close($OUT);

```

The code just explains itself.

Bingo!
