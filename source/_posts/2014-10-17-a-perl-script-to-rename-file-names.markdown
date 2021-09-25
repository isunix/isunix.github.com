---
layout: post
title: "Perl脚本批量重命名文件"
date: 2014-10-17 16:15:19 +0800
comments: true
categories: Perl
---
I have some files with file name quite weird in the format, "[Alex_Holmes]_Hadoop_in_Practice(BookZZ.org).pdf
". What I want to achieve is removing the parts in the [] or ().  Here below is the perl script I wrote. 

```pl
use strict;
use warnings;
use Data::Dumper;
use Cwd;

my $target_dir = getcwd();

opendir(my $dh, $target_dir) || die "can't opendir $target_dir: $!";

my @files = grep { /\w/ && -f "$_" && !/^\./} readdir($dh);
# [Alex_Holmes]_Hadoop_in_Practice(BookZZ.org).pdf
#files not staring with "." and contains char, thus (., .., .DS_STORE) will be ignored.
#print Dumper @files;

for(@files){
    my $file = $_;
    if(/^(?:\[[\S\s]+\])([\S\s]+)(?:\([\S\s]+\))\.pdf$/){
        my $new_name = $1.".pdf";
        rename("$file", "$new_name") || die("error in renaming: $!");
    }
}
```