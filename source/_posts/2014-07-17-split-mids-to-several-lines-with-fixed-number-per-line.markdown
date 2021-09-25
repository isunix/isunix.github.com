---
layout: post
title: "将一个每行一个item的多行文本转变成每行固定数目的item的文本(PHP)"
date: 2014-07-17 10:26:09 +0800
comments: true
categories: PHP
---
We have many mids with one mid every line, now we want to print all those mids out with a fixed number of mids per line. I want to realize this function in Perl first without success, so I am using PHP. 

```php 

<?php

$scriptname = $argv[0];
$txt_file = $argv[1];
$dir = ".";

$contents = file_get_contents("$dir/$txt_file", FILE_USE_INCLUDE_PATH);
$contents = trim($contents);

$mid_splited = preg_split("/\n/", $contents);

$count_mids = count($mid_splited);

for ($i = 0; $i < $count_mids; $i++){
  print "$mid_splited[$i] ";
  if ($i % 7 == 0){
    print "\n";
  }
}


?>

```　