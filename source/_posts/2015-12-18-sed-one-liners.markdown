---
layout: post
title: "sed one-liners"
date: 2015-12-18 14:48:18 +0800
comments: true
categories: Shell
---
The following is a collection of sed. They are from the following blogs.

```html
http://www.catonmat.net/blog/sed-one-liners-explained-part-one/
http://www.catonmat.net/blog/sed-one-liners-explained-part-two/
http://www.catonmat.net/blog/sed-one-liners-explained-part-three/

http://www.grymoire.com/Unix/Sed.html
http://www.catonmat.net/blog/wp-content/uploads/2008/09/sed1line.txt
```

I will pick some I that I think might be useful for me and listed them here.

1.Insert a blank line above every line that matches "regex".

```sh
cat file | sed '/regex/{x;p;x;}'
```

2.Insert a blank line below every line that matches "regex".

```sh
cat file | sed '/regex/G'
```

3.Insert a blank line above and below every line that matches "regex".

```sh
cat file | sed '/regex/{x;p;x;G;}'
```

4.Number each line of a file (named filename). Left align the number.

```sh
sed = filename | sed 'N;s/\n/\t/'
```

5.Convert DOS/Windows newlines (CRLF) to Unix newlines (LF). (All 3 have not been tested!)

```sh
cat file | sed 's/.$//'
cat file | sed 's/^M$//'
cat file | sed 's/\x0D$//'
```

6.Convert Unix newlines (LF) to DOS/Windows newlines (CRLF). (All 3 have not been tested!)

```sh
sed 's/$/\r/'
sed "s/$//"
sed "s/$/`echo -e \\\r`/"
```

7.Delete leading whitespace (tabs and spaces) from each line.

```sh
cat file | sed 's/^[ \t]*//'
```

8.Delete trailing whitespace (tabs and spaces) from each line.

```sh
cat file | sed 's/[ \t]*$//'
```

9.Delete both leading and trailing whitespace from each line.

```sh
cat file | sed 's/^[ \t]*//;s/[ \t]*$//'
```

10.Insert five blank spaces at the beginning of each line.

```sh
cat file | sed 's/^/     /'
```

11.Substitute (find and replace) the fourth occurrence of "foo" with "bar" on each line.

```sh
cat file | sed 's/foo/bar/4'
```

12.Substitute (find and replace) the first occurrence of a repeated occurrence of "foo" with "bar".

```sh
cat file | sed 's/\(.*\)foo\(.*foo\)/\1bar\2/'
```

13.Substitute all occurrences of "foo" with "bar" on all lines that contain "baz".

```sh
cat file | sed '/baz/s/foo/bar/g'
```

14.Substitute all occurrences of "foo" with "bar" on all lines that DO NOT contain "baz".

```sh
cat file | sed '/baz/!s/foo/bar/g'
```

15.Change text "scarlet", "ruby" or "puce" to "red".

```sh
cat file | sed 's/scarlet/red/g;s/ruby/red/g;s/puce/red/g'
```

16.Add a blank line after every five lines.

```sh
cat file | sed 'n;n;n;n;G;'
```

17.Print the first 10 lines of a file (emulates "head -10").

```sh
cat file | sed 10q
```

18.Print only the lines that match a regular expression (emulates "grep").

```sh
cat file | sed -n '/regexp/p'
```

19.Print only the lines that do not match a regular expression (emulates "grep -v").

```sh
cat file | sed -n '/regexp/!p'
```

20.Print the line immediately before regexp, but not the line containing the regexp.

```sh
cat file | sed -n '/regexp/{g;1!p;};h'
```

21.Print the line immediately after regexp, but not the line containing the regexp.

```sh
cat file | sed -n '/regexp/{n;p;}'
```

22.Print one line before and after regexp. Also print the line matching regexp and its line number. (emulates "grep -A1 -B1").

```sh
cat file | sed -n -e '/regexp/{=;x;1!p;g;$!N;p;D;}' -e h
```

23.Grep for "AAA" and "BBB" and "CCC" in any order.

```sh
cat file | sed '/AAA/!d; /BBB/!d; /CCC/!d'
```

24.Grep for "AAA" and "BBB" and "CCC" in that order.

```sh
cat file | sed '/AAA.*BBB.*CCC/!d'
```

25.Grep for "AAA" or "BBB", or "CCC".

```sh
cat file | sed -e '/AAA/b' -e '/BBB/b' -e '/CCC/b' -e d
```

26.Print only the lines that are 65 characters in length or more.

```sh
cat file | sed -n '/^.\{65\}/p'
```

27.Print only the lines that are less than 65 chars.

```sh
cat file | sed '/^.\{65\}/d'
```

28.Print section of a file from a regex to end of file.

```sh
cat file | sed -n '/regexp/,$p'
```

29.Print lines 8-12 (inclusive) of a file.

```sh
cat file | sed -n '8,12p'
```

30.Print line number 52.

```sh
cat file | sed -n '52p'
```

31.Beginning at line 3, print every 7th line.

```sh
cat file | sed -n '3,${p;n;n;n;n;n;n;}'
```

32.Print section of lines between two regular expressions (inclusive).

```sh
cat file | sed -n '/Iowa/,/Montana/p'
```

33.Print all lines in the file except a section between two regular expressions.

```sh
cat file | sed '/Iowa/,/Montana/d'
```

34.Delete duplicate, consecutive lines from a file (emulates "uniq").

```sh
cat file | sed '$!N; /^\(.*\)\n\1$/!P; D'
```

35.Delete all lines except duplicate consecutive lines (emulates "uniq -d").

```sh
cat file | sed '$!N; s/^\(.*\)\n\1$/\1/; t; D'
```

36.Delete the first 10 lines of a file.

```sh
cat file | sed '1,10d'
```

37.Delete the last line of a file.

```sh
cat file | sed '$d'
```

38.Delete the last 2 lines of a file.

```sh
cat file | sed 'N;$!P;$!D;$d'
```

39.Delete lines that match regular expression pattern.

```sh
cat file | sed '/pattern/d'
```

40.Delete all blank lines in a file (emulates "grep '.'".

```sh
cat file | sed '/^$/d'
```

41.Delete all consecutive blank lines from a file (emulates "cat -s").

```sh
cat file | sed '/./,/^$/!d'
```

42.Delete all leading blank lines at the top of a file.

```sh
cat file | sed '/./,$!d'
```

43.Delete all trailing blank lines at the end of a file.

```sh
cat file | sed -e :a -e '/^\n*$/{$d;N;ba' -e '}'
```