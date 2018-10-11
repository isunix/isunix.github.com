---
layout: post
title: "Regexp::Debugger使用示例"
date: 2014-10-09 14:09:52 +0800
comments: true
categories: Perl
---
This post shows how to use the perl module, Regexp::Debugger. Used skillfully, this module can do us a lot of favor.  

1."rxrx prog.pl" is a shorthand for "perl -MRegexp::Debugger prog.pl".  


2.print out if matched
 
```pl
perl -E "say 'matched' if 'ababc' =~ /(a|b)b+c/x"
```  


3.print out if matched and which part matched

```pl
perl -E "say 'matched: ', $& if 'ababc' =~ /(a|b)b+c/x"
```

4.use "re" module

```pl
perl -E "use re 'debug'; 'ababc' =~ /(a|b)b+c/x"
```  

5.use Regexp::Debugger module

```pl
perl -E "use Regexp::Debugger; 'ababc' =~ /(a|b)b+c/x"
```  

6.any regex

```pl
(?i) (?<AB> (?&ABs)) (?<AA>(??{'aa'})) (?(DEFINE)(?<ABs>[ab]{2,7}+))/
```

7.for the Regexp::Debugger, we have a cmd-line tool named "rxrx", we typr "rxrx", then

```pl
/(a|b)b+c/
"ababc"
```

Then hit "enter" key or "tab" key to see how and if the string matches the regex.

