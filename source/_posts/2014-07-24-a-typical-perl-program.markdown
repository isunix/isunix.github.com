---
layout: post
title: "a typical perl program"
date: 2014-07-24 15:17:20 +0800
comments: true
categories: Perl
---
Of courese there are many perl programms that can be claimed as "typical", yet you can not what is truely "typical". The one below is where I met in the book "perl for dummies". Ok, show you the code now.   

```perl  

$TheFile = "sample.txt";

open(INFILE, $TheFile) or die "The file $TheFile could " .  "not be found.\n";

$CharCount = 0;
$WordCount = 0;
$LineCount = 0;

while(<INFILE>) {
  $TheLine = $_;
  chomp($TheLine);
  
  $LineCount = $LineCount + 1;
  $LineLen = length($TheLine);
  $CharCount = $CharCount + $LineLen;
  
  if($TheLine eq "") { next }; ##evaluate the next line;
  $WordCount = $WordCount + 1;
  $CharPos = 0;
  
  until($CharPos == $LineLen) {
    if(substr($TheLine, $CharPos, 1) eq " ")
      { $WordCount = $WordCount + 1 }
    $CharPos = $CharPos + 1;
  }
}

print "For the file $TheFile:\n";
print "Number of characters $CharCount\n";
print "Number of words    $WordCount\n";
print "Number of lines    $LineCount\n";

```    

I list this program here, because We can learn how to use chomp, length, $_, <>, until, next, eq, ==, next, substr, FILEHANDLE, string concatenation, how to tell if it is a word and so on, all these import concepts in perl programming in one script. 