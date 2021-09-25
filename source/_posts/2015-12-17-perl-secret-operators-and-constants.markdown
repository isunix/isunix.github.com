---
layout: post
title: "Perl中的秘密(secret) operators和constants"
date: 2015-12-17 10:37:47 +0800
comments: true
categories: Perl
---
Several days I met some perl one-liner like this:

```sh
cat $file | perl -Mautodie -MList::MoreUtils=none -ne 'chomp; push @re, $_ }{ open $fh, $ENV{CF}; @s = <$fh>; foreach $s (@s) { print $s if none { $s =~ qr/$_/ } @re };'
```

I have no idea what the "}{" here means, at first I thought it maybe some typo.

Then my colleagues showed me the following page, which lists many weird perl operators.

```html
http://search.cpan.org/dist/perlsecret/lib/perlsecret.pod
```

To have a look at how it is used in the backend:

```sh
$ perl -MO=Deparse -lne '}{print$.'
```

It will give the following code:

```perl
-e syntax OK
    BEGIN { $/ = "\n"; $\ = "\n"; }
    LINE: while (defined($_ = <ARGV>)) {
        chomp $_;
    }
    {
        print $.;
    }
```