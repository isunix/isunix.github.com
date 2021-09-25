---
layout: post
title: "Perl的一行命令(one-liner)"
date: 2015-12-11 10:18:24 +0800
comments: true
categories: Perl
---
Some maybe useful perl one-liners here for easy reference.

Some of the tip are from the post:

```html
http://www.catonmat.net/blog/perl-one-liners-explained-part-one/
```

Some are from my own daily usage.

I also found there are posts about useful sed/awk/perl one-liners:

```html
http://www.catonmat.net/blog/awk-one-liners-explained-part-one/
http://www.catonmat.net/blog/sed-one-liners-explained-part-one/
http://www.catonmat.net/blog/introduction-to-perl-one-liners/
http://linux.gda.pl/spotkania/sp_13/perl-one-liners.pdf
```

1.Loop through a file for each line to find the lines matching certain pattern. Then grep those pattern against a file, and print those lines which has a column meets certain criteria.

```sh
cat file1.txt | perl -nle 'print $1 if /\b(__[0-9a-z]\w+)\b/i;' | sort | uniq | xargs -I , grep , -w fileb.txt | awk '$2==0' | awk '{print $7}' | sort | uniq | xargs -I , grep , -w filec.txt | awk '$8==0' | awk '{print $8," ",$13}' > /tmp/`date +%Y%m%d`.txt
```

2.Add a blank line before every line.

```sh
perl -pe 's//\n/' file.txt
```

3.Remove all blank lines

```sh
cat file.txt | perl -ne 'print unless /^$/'
```

4.Remove all consecutive blank lines, leaving just one.

```sh
cat file.txt | perl -00 -pe ''
```

5.Compress/expand all blank lines into N consecutive ones.

```sh
cat 1.txt| perl -00 -pe '$_.="\n"x4'
```

6.substitute something in a file:

```sh
perl -pi -e 's/good/bad/g' file.txt
```

7.same as item-6 but only on lines match something:

```sh
perl -pi -e 's/good/bad/g if /matched/' file
```

8.Finding all repeated lines in a file:

```sh
perl -ne 'print if $a{$_}++' 1.txt
```

9.Numbering lines in a file:

```sh
perl -ne 'print "$. $_"' file.txt
```
or with the '-p' argument:

```sh
perl -pe '$_ = "$. $_"' file.txt
```

10.Sum up all the numbers on each line:

```sh
cat file.txt| perl -MList::Util=sum -alne 'print sum @F'
```

11.TO see how the above one-liner works, use the Data::Dumper module to get a look at it:

```sh
cat file.txt| perl -MData::Dumper -alne 'print  Dumper @F'
```

12.Finding the date 10 days ago:

```sh
perl -MPOSIX -le '@now = localtime; $now[3] -= 10; print scalar localtime mktime @now'
```

13.Find the sum of the numbers in the first column:

```sh
cat file.txt| perl -lane '$sum += $F[0]; END { print $sum }'
```

14.Getting a list of the names of all users on the system:

```sh
perl -a -F: -lne 'print $F[4]' /etc/passwd
```

15.Print the number of non-empty lines in a file:

```sh
cat file.txt | perl -le 'print scalar(grep{/./}<>)'
```

16.Print the number of empty lines in a file:

```sh
cat file.txt| perl -lne '$a++ if /^$/; END {print $a+0}'
```

or 

```sh
cat file.txt | perl -le 'print scalar(grep{/^$/}<>)'
```

or 

```sh
cat file.txt | perl -le 'print ~~grep{/^$/}<>'
```

17.Print the number of lines in a file that match a pattern (emulate grep -c):

```sh
cat 3.txt| perl -lne '$a++ if /good/; END {print $a+0}'
```

or 

```sh
cat 3.txt | grep -c "good"
```

18.Generate and print the alphabet:

```sh
perl -le 'print ("a".."z")'
or 
perl -le 'print a..z'
or 
perl -le 'print join "", ("a".."z")'
```

19.Generate a random 8 character password:

```sh
perl -le 'print map { ("a".."z")[rand 26] } 1..8'
```

20.Find the numeric values for characters in the string:

```sh
perl -le 'print join ", ", map { ord } split //, "hello world"'
```

21.Generate an array with odd numbers from 1 to 100:

```sh
perl -le '@odd = grep {$_ % 2 == 1} 1..100; print "@odd"'
```

22.Find the length of the string:

```sh
perl -le 'print length "hello boy"'
```

23.Find the number of elements in an array:

```sh
perl -le '@array = ("a".."z"); print ~~@array'
or
perl -le '@array = ("a".."z"); print scalar @array'
or 
perl -le '@array = ("a".."z"); print $#array + 1'
```

24.Base64 encode a string:

```sh
perl -MMIME::Base64 -e 'print encode_base64("string")'
```

25.base64 encode the whole file:

```sh
perl -MMIME::Base64 -0777 -ne 'print encode_base64($_)' file
```

26.Base64 decode a string:

```sh
perl -MMIME::Base64 -le 'print decode_base64("c3RyaW5n")'
```

27.URL-escape a string:

```sh
perl -MURI::Escape -le 'print uri_escape("1+2")'
```

28.URL-unescape a string:

```sh
perl -MURI::Escape -le 'print uri_unescape("1%2B2")'
```

29.HTML-encode a string:

```sh
perl -MHTML::Entities -le 'print encode_entities("<br>")'
```

30.HTML-decode a string:

```sh
perl -MHTML::Entities -le 'print decode_entities("&lt;br&gt;")'
```

31.Convert all text to uppercase:

```sh
cat file | perl -nle 'print uc'
```

32.Camel case each line:

```sh
cat file | perl -ple 's/(\w+)/\u$1/g'
```

33.Strip leading whitespace (spaces, tabs) from the beginning of each line:

```sh
cat file | perl -ple 's/^[ \t]+//'
```

34.Strip trailing whitespace (space, tabs) from the end of each line:

```sh
cat file | perl -ple 's/[ \t]+$//'
```

35.Strip whitespace from the beginning and end of each line:

```sh
cat file | perl -ple 's/^[ \t]+|[ \t]+$//g'
```

36.Substitute (find and replace) "foo" with "bar" on lines that match "baz":

```sh
cat file | perl -pe '/baz/ && s/foo/bar/'
```

37.Print the first line of a file (emulate head -1):

```sh
cat file | perl -ne 'print; exit'
```

38.Print the first 10 lines of a file (emulate head -10):

```sh
perl -ne 'print if $. <= 10'
```

This one-liner uses the $. special variable. This variable stands for "current line number." 

39.Print the last line of a file:

```sh
cat file | perl -ne '$last = $_; END { print $last }'
or
cat file | perl -ne 'print if eof'
```

40.Print the last 10 lines of a file (emulate tail -10):

```sh
cat file | perl -ne 'push @a, $_; @a = @a[@a-10..$#a]; END { print @a }'
```

41.Print only lines that do not match a regular expression:

```sh
cat file | perl -ne '!/regex/ && print'
```

42.Print the line before a line that matches a regular expression:

```sh
cat file | perl -ne '/regex/ && $last && print $last; $last = $_'
```

43.Print the line after a line that matches a regular expression:

```sh
cat file | perl -ne 'if ($p) { print; $p = 0 } $p++ if /regex/'
```

44.Print lines that match regex AAA and regex BBB in any order:

```sh
cat file | perl -ne '/AAA/ && /BBB/ && print'
```

45.Print lines that don't match match regexes AAA and BBB:

```sh
cat file | perl -ne '!/AAA/ && !/BBB/ && print'
```

46.Print lines that match regex AAA followed by regex BBB followed by CCC:

```sh
cat file | perl -ne '/AAA.*BBB.*CCC/ && print'
```

47.Print lines that are 20 chars or longer:

```sh
cat file | perl -ne 'print if length >= 80'
```

48.Print only line 13:

```sh
cat file | perl -ne '$. == 13 && print && exit'
```

49.Print all lines except line 13.

```sh
perl -ne '$. != 13 && print'
```

50.Print only lines 13, 19 and 67:

```sh
perl -ne 'print if $. == 13 || $. == 19 || $. == 67'
```

51.Print all lines between two regexes:

```sh
cat file | perl -ne 'print if /regex1/../regex2/'
```

52.Print all lines from line 17 to line 30:

```sh
cat file | perl -ne 'print if $. >= 17 && $. <= 30'
```

53.Print the longest line:

```sh
cat file | perl -ne '$l = $_ if length($_) > length($l); END { print $l }'
```

54.Print the shortest line:

```sh
cat file | perl -ne '$s = $_ if $. == 1; $s = $_ if length($_) < length($s); END { print $s }'
```

55.Print all lines that contain only characters:

```sh
cat file | perl -ne 'print if /^[[:alpha:]]+$/'
```

56.Print all lines that repeat:

```sh
cat file | perl -ne 'print if ++$a{$_} == 2'
```

57.Print all unique lines:

```sh
cat file | perl -ne 'print unless $a{$_}++'
```

58.To remove blank lines:

```sh
cat file | perl -pi -e 's!^\s+?$!!'
```