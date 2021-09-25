---
layout: post
title: "ubuntu中删除孤立的包"
date: 2015-06-02 10:03:32 +0800
comments: true
categories: Perl
---
After upgrading ubuntu to a new version, there will be many obsolete packages. To see these packages, you can 

```bash
sudo apt-get upgrade
```
It will list all those obsolete packages.

To autoremove them one by one will be will tedious, we can first copy those packages into a file, like aa.txt, then use the following perl script to do it once:

```pl
use File::Slurp;
my @modules;
my $text = read_file('aa.txt', text_ref => 1);
@modules = grep {not /\s+/} split('[\s+]', $text);
foreach my $module (@modules){
	system("sudo apt-get autoremove $module");
}
```

Done!
