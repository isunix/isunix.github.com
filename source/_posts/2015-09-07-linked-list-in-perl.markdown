---
layout: post
title: "Linked List in Perl"
date: 2015-09-07 12:30:05 +0800
comments: true
categories: perl
---
We will use linked list to output words in a file in alphabetical order. This example is in:
```
http://man.ddvip.com/web/perl/perl9.htm#10.1
```

```pl
use utf8;

$header = "";
while ( $line = <STDIN> ) {
    chomp;
    @words = split( /\s+/, $line );
    foreach my $word (@words) {
        ##remove punctuation and transform from uppercase to lower case.

        $word =~ s/[,.:;-]//;
        $word =~ tr/A-Z/a-z/;
        &add_word_to_list($word);
    }
}

&print_list;

sub add_word_to_list {

    #these two are lists.
    my ($word) = @_;
    my ($pointer);

    # if list is empty, add first item;
    if ( $header eq "" ) {
        $header = $word;
        $wordlist{$word} = "";
        return;
    }

    # if word identical to first element in list, do nothing
    return if ( $header eq $word );

    # to see if word should be the new first word in the list.

    if ( $header gt $word ) {
        $wordlist{$word} = $header;
        $header = $word;
        return;
    }

    # find place where the word belongs
    $pointer = $header;
    while ( $wordlist{$pointer} ne "" && $wordlist{$pointer} lt $word ) {
        $pointer = $wordlist{$pointer};
    }

    # if the word seen already, do nothing
    return if ( $word eq $wordlist{$pointer} );
    $wordlist{$word}    = $wordlist{$pointer};
    $wordlist{$pointer} = $word;
}

sub print_list {
    local ($pointer);
    print("Words in the input are:\n");
    $pointer = $header;
    while ( $pointer ne "" ) {
        print("$pointer\n");
        $pointer = $wordlist{$pointer};
    }
}
```

and for a tree structure:

```pl
use utf8;

my $rootname = "parent";

my %tree = (
    "parentleft", "child1",      "parentright", "child2",
    "child1left", "grandchild1", "child1right", "grandchild2",
    "child2left", "grandchild3", "child2right", "grandchild4"
);

# traverse tree, printing its elements
&print_tree($rootname);

sub print_tree {
    local ($nodename) = @_;
    local ( $leftchildname, $rightchildname );

    $leftchildname  = $nodename . "left";
    $rightchildname = $nodename . "right";

    # this is a left-order traversal.

    if ( $tree{$leftchildname} ne "" ) {
        &print_tree( $tree{$leftchildname} );
    }
    print("$nodename\n");

    if ( $tree{$rightchildname} ne "" ) {
        &print_tree( $tree{$rightchildname} );
    }
}
```