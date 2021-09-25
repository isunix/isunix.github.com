---
layout: post
title: "使用Perl脚本从文件中找需要的信息"
date: 2014-07-24 15:33:54 +0800
comments: true
categories: Perl
---
This one is where I excerpted from the book "perl for dummies".  

```perl

$TheDB = 'edata.txt';


open(INDB, $TheDB) or die "The database $TheDB could " . "not be found.\n";

while(1) { 

  print "\nDo you want to search by employee ID (I), " . " or quit (Q): ";
  
  $DoSearch = <STDIN>;
  chomp($DoSearch);
  $DoSearch =~ tr/A-Z/a-z/;
  
  if($DoSearch eq 'q') { last }
  
  unless($DoSearch eq 'i') {
    print "You must enter either I or Q.\n";
    next; 
  }
  
  print "Search for ID number: ";
  $SearchFor = <STDIN>;
  chomp($SearchFor);
    
  seek(INDB, 0, 0);   ##search from the beginning of file.
  
  $SuccessCount = 0;
  
  while(<INDB>) {
    $TheRec = $_;
    chomp($TheRec);
    ($LastName, $FirstName, $ID, $Tel) =
      split(/\t/, $TheRec);
    if($ID eq $SearchFor) {
      $SuccessCount = $SuccessCount + 1;
      print "$ID: $FirstName $LastName, ext. ". "$Tel\n";
    } 
  } 
  
  if($SuccessCount == 0) { print "No records found.\n" }
  else { print "$SuccessCount records found.\n" }
} 

print "Program finished.\n";

```
We can learn the use of while, endless loop, file-handle, last, tr, seek, $_, eq, split, string concatenation if-else, chomp, ==, eq all these things in one perl script.  

