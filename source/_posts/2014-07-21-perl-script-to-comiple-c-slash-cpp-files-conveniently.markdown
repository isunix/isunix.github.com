---
layout: post
title: "使用Perl来更加方便地编译c/cpp文件"
date: 2014-07-21 21:31:33 +0800
comments: true
categories: Perl
---
我自己在编译c还有c++文件的时候， 总感觉每次都得敲像下面这种格式的一串字符， 感觉很麻烦的。   

```c
gcc -o hello hello.c

```

所以就有了现在的这个脚本。使用方法很简单，想上面这个hello.c的文件，我们只要发出下面的命令:    

```c

cpl hello.c   

```

就可以编译出来一个去掉以原来的文件名去掉ext的文件。  

很简单吧！哈哈！  

下面给出来代码， 还是继续把doc写进去的那种。

```perl

use 5.010;
use strict;
use warnings;
use utf8;
use Cwd;
use File::Basename;

my $currentDir = getcwd;
my $file = $ARGV[0];
my $fullpath = "$currentDir/$file";
my @suffix_list = qw(.cpp .c);

my ($name, $dir, $ext) = fileparse($file, @suffix_list);
given($ext){

    when(".c"){
        my $compile_c = "gcc -o $name $file";
        system($compile_c);
    }

    when(".cpp"){
        my $compile_cpp = "g++ -o $name $file";
        system($compile_cpp);
    }

    default{
        say "$file is of an type not compilable!";
    }
}

__END__
=pod

=head1 NAME

cpl

=head1 SYNOPSIS
    $ cpl filename

cpl --use gcc/g++ to compile a file with c/cpp extension. Usually we will do things like "gcc -o hello hello.c", but with this scipt, we can just issue command like this, "gcp hello.c";

Thanks,
Steven

```
