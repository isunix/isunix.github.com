---
layout: post
title: "perl script to delete files without extension"
date: 2014-07-21 18:18:34 +0800
comments: true
categories: Perl
---
I want to delete those files without the extension I need, so I just write this perl script. The directory can also be specified on the command line. I list all those extensions I need as a pattern.

```perl
use strict;
use warnings;
use utf8;
use Cwd;

my $targetDir = $ARGV[0] || getcwd;
chdir $targetDir;

my $pattern = qr/\.(md|py|php|sh|bash|zsh|vimrc|eamcs|c|cpp|java|pl|js|css|html|rb|txt)$/i,
my @file_list;


opendir(my $dh, $targetDir) || die "can't opendir $targetDir: $!";
while (readdir $dh){
    next unless -f;
    next if $_ =~ $pattern;
    push @file_list, $_;
}
closedir $dh;

print "The following files are going to be deleted: @file_list\n";
unlink @file_list;

__END__
=pod

=head1 NAME

delete-files.pl -delete those files without the extension as specifed in the pattern

=head1 SYNOPSIS

    $ delete-files
It reads the files in the directory where you execute this script, and delete those
not having the extension as is specified "(md|py|php|sh|bash|zsh|vimrc|eamcs|c|cpp|java|pl|js|css|html|rb|txt)"

Please use this script carefully. If you have somefile without extension which you also
consider them important, they maybe deleted.

Thanks,
Steven

=cut


```

I also wrote document for this scirpt. haha!
