---
layout: post
title: "useful awk commands"
date: 2015-12-21 16:51:15 +0800
comments: true
categories: Shell
---
The following blogs are referenced, 

```
http://www.catonmat.net/blog/awk-one-liners-explained-part-one/
```

And I will list some of the commands I think might be useful for later usage here.

* Print the total number of lines containing word "Regex".

```sh
cat file | awk '/Regex/ { n++ }; END { print n+0 }'
```

* Print every line with more than 4 fields.

```sh
cat file | awk 'NF > 4'
```

* Print every line where the value of the last field is greater than 4.

```sh
cat file | awk '$NF > 4'
```

* Convert Windows/DOS newlines (CRLF) to Unix newlines (LF) from Unix.

```sh
cat file | awk '{ sub(/\r$/,""); print }'
```

* Convert Unix newlines (LF) to Windows/DOS newlines (CRLF) from Unix.

```sh
cat file | awk '{ sub(/$/,"\r"); print }'
```

* Delete leading whitespace (spaces and tabs) from the beginning of each line (ltrim).

```sh
cat file | awk '{ sub(/^[ \t]+/, ""); print }'
```

* Delete trailing whitespace (spaces and tabs) from the end of each line (rtrim).

```sh
cat file | awk '{ sub(/[ \t]+$/, ""); print }'
```

* Delete both leading and trailing whitespaces from each line (trim).

```sh
cat file | awk '{ gsub(/^[ \t]+|[ \t]+$/, ""); print }'
```

* Insert 5 blank spaces at beginning of each line.

```sh
cat file | awk '{ sub(/^/, "     "); print }'
```

* Center all text on a 79-character width.

```sh
cat file | awk '{ l=length(); s=int((79-l)/2); printf "%"(s+l)"s\n", $0 }'
```

* Substitute (find and replace) "foo" with "bar" on each line.

```sh
cat file | awk '{ sub(/foo/,"bar"); print }'
```

* Substitute "foo" with "bar" only on lines that contain "baz".

```sh
cat file | awk '/baz/ { gsub(/foo/, "bar") }; { print }'
```

* Substitute "foo" with "bar" only on lines that do not contain "baz".

```sh
cat file | awk '!/baz/ { gsub(/foo/, "bar") }; { print }'
```

* Change "scarlet" or "ruby" or "puce" to "red".

```sh
cat file | awk '{ gsub(/scarlet|ruby|puce/, "red"); print}'
```

* Reverse order of lines (emulate "tac").

```sh
cat file | awk '{ a[i++] = $0 } END { for (j=i-1; j>=0;) print a[j--] }'
```

* Swap first field with second on every line.

```sh
cat file | awk '{ temp = $1; $1 = $2; $2 = temp; print }'
```

* Delete the second field on each line.

```sh
cat file | awk '{ $2 = ""; print }'
```

* Print the fields in reverse order on every line.

```sh
cat file | awk '{ for (i=NF; i>0; i--) printf("%s ", $i); printf ("\n") }'
```

* Remove duplicate, consecutive lines (emulate "uniq")

```sh
cat file | awk 'a !~ $0; { a = $0 }'
```

* Remove duplicate, nonconsecutive lines.

```sh
cat file | awk '!a[$0]++'
```

* Concatenate every 5 lines of input with a comma.

```sh
cat file | awk 'ORS=NR%5?",":"\n"'
```

* Print only the lines that match a regular expression "/regex/" (emulates "grep").

```sh
cat file | awk '/regex/'
```

* Print only the lines that do not match a regular expression "/regex/" (emulates "grep -v").

```sh
cat file | awk '!/regex/'
```

* Print the line immediately before a line that matches "/regex/" (but not the line that matches itself).

```sh
cat file | awk '/regex/ { print x }; { x=$0 }'
```

* Print the line immediately after a line that matches "/regex/" (but not the line that matches itself).

```sh
cat file | awk '/regex/ { getline; print }'
```

* Print lines that match any of "AAA" or "BBB", or "CCC".

```sh
cat file | awk '/AAA|BBB|CCC/'
```

* Print lines that contain "AAA" and "BBB", and "CCC" in this order.

```sh
cat file | awk '/AAA.*BBB.*CCC/'
```

* Print only the lines that are 65 characters in length or longer.

```sh
cat file | awk 'length > 64'
```

* Print a section of file from regular expression to end of file.

```sh
cat file | awk '/regex/,0'
```

* Print lines 8 to 12 (inclusive).

```sh
cat file | awk 'NR==8,NR==12'
```

* Print line number 52.

```sh
cat file | awk 'NR==52'
```

* Print section of a file between two regular expressions (inclusive).

```sh
cat file | awk '/Iowa/,/Montana/'
```

* Delete all blank lines from a file.

```sh
cat file | awk NF
``` 

This one-liner uses the special NF variable that contains number of fields on the line. For empty lines, NF is 0, that evaluates to false, and false statements do not get the line printed.

* Create a string of a specific length (generate a string of x's of length 513).

```sh
awk 'BEGIN { while (a++<513) s=s "x"; print s }'
```

* Insert a string of specific length at a certain character position (insert 49 x's after 6th char).

```sh
gawk --re-interval 'BEGIN{ while(a++<49) s=s "x" }; { sub(/^.{6}/,"&" s) }; 1'
```

* Print all lines where 5th field is equal to "abc123".
```sh
cat file | awk '$5 == "abc123"'
```

* Print any line where field #5 is not equal to "abc123".

```sh
cat file | awk '$5 != "abc123"'
```

* Print all lines whose 7th field matches a regular expression.

```sh
cat file | awk '$7  ~ /^[a-f]/'
or 
cat file | awk '$7 !~ /^[a-f]/'
```


