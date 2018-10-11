---
layout: post
title: "make array into string using perl"
date: 2014-11-27 16:49:04 +0800
comments: true
categories: Perl
---
In perl, there are cases we may want to make an array into string, and then for the string, we may also want to change it to the format that we want to use. Here below are some exaples. 

Say we have an array, 

```pl
my @nums = (1234, 5678, 2345, 8976);
```

And we then want to change it to a string with comma separated followed by a blank space.  

```pl
my $nums = join ", ", @nums;
```

We then want to use the nums in a sql "in" clause which will have the format, 

```sql
select * from table where column in (1234, 5678, 2345, 8976);
```

Of course we can not use the array @nums here, we can change the $nums to the format, 

```pl
$nums_in_str = "(" . join( ",", @nums ) . ")";
```

Then we can do the sql query as the following:  

```sql
select * from table where column in $nums_in_str
```

That's it!