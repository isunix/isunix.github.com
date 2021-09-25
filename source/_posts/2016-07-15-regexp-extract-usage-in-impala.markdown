---
layout: post
title: "impala里使用regexp_extract函数"
date: 2016-07-15 10:43:30 +0800
comments: true
categories: BigData
---
I need to use the regexp_extract function to extract certain parts of a string recently when I am doing big data analysis.

http://www.cloudera.com/documentation/archive/impala/2-x/2-1-x/topics/impala_string_functions.html, this link shows us how to do, but sadly regex in impala is a little different from those in perl or python, so I have to look through the page and try again.

I keep a note here for regexp_extract for my later own usage.

Say I have a string 

```
%2C%22hidisp%22%3A27%2C%22quietMode
```

and I want to extract the number followd by "hidisp" and '":', which is number '27' here.

As describe in the above document, 

```
Because the impala-shell interpreter uses the \ character for escaping, use \\ to represent the regular expression escape character in any regular expressions that you submit through impala-shell
```

So if we want to represent the numbers here, we have use '\\d' rather than just '\d' which is a standard in other programming  languages.


regexp_extract usage is in the following format,

```
regexp_extract(string subject, string pattern, int index)
```

1. group 0 matches the full pattern string, including the portion outside any () group, so

```
select regexp_extract('%2C%22hidisp%22%3A27%2C%22quietMode', 'hidisp%22%3A(\\d+)', 0);
```

this will give out:

```
hidisp%22%3A27
```

2. group 1 matches just the contents inside the first () group in the pattern string:

```
select regexp_extract('%2C%22hidisp%22%3A27%2C%22quietMode', 'hidisp%22%3A(\\d+)', 1);
```

will give out

```
27
```

And for the support of non-greedy matches using .*?, take the following string as an example,

```
%2C%22reboot%22%3A27%2C%22quietMode%2C%22reboot%22%3A12%2C%22quietMode
```

How to extract the first match number for "reboot", we can get the result in the following ways

a. without any ".*?" around the string pattern 'reboot%22%3A(\\d+)', which is the easiest way I think 

```
select regexp_extract('%2C%22reboot%22%3A27%2C%22quietMode%2C%22reboot%22%3A12%2C%22quietMode', 'reboot%22%3A(\\d+)', 1);
```

or 

b. append ".*?" right after the string pattern 'reboot%22%3A(\\d+)',

```
select regexp_extract('%2C%22reboot%22%3A27%2C%22quietMode%2C%22reboot%22%3A12%2C%22quietMode', 'reboot%22%3A(\\d+).*?', 1);
```

or

c. surround the string pattern 'reboot%22%3A(\\d+)' with '.*?' at both sides

```
select regexp_extract('%2C%22reboot%22%3A27%2C%22quietMode%2C%22reboot%22%3A12%2C%22quietMode', '.*?reboot%22%3A(\\d+).*?', 1);
```

So after the tree ways to get the leftmost match, we can easily guess how to get the rifht-most match.

```
select regexp_extract('%2C%22reboot%22%3A27%2C%22quietMode%2C%22reboot%22%3A12%2C%22quietMode', '.*?reboot%22%3A(\\d+)', 1);
```

That is just by appending the string pattern with '.*?' at its left side.