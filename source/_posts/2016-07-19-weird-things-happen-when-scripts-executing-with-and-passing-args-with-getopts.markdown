---
layout: post
title: "bash中getopts使用备忘"
date: 2016-07-19 17:43:32 +0800
comments: true
categories: Shell
---
I have met the following scripts, say aa.sh

```sh
echo "OPTIND for aa.sh before calling is: " $OPTIND
while getopts "t:c:" opt
do
    case "$opt" in
        t) time="${OPTARG}";;
        c) count="${OPTARG}";;
    esac
done

echo "time for aa.sh is $time"
echo "count for aa.sh is $count"
echo "OPTIND for aa.sh after calling is: " $OPTIND`sh
```

and bb.sh

```sh
echo "OPTIND for bb.sh before calling is: " $OPTIND
echo "we are setting the OPTIND to 1"
while getopts "t:c:" opt
do
    case "$opt" in
        t) time="${OPTARG}";;
        c) count="${OPTARG}";;
    esac
done

echo "time for bb.sh is $time"
echo "count for bb.sh is $count"

echo "OPTIND for bb.sh after calling is: " $OPTIND
```

and call.sh

```sh
. ./aa.sh -t 2016-07-15 -c 4
. ./bb.sh -a 2016-07-20 -c 0
```

and now execute the script, it will give out the followig result,

```
OPTIND for aa.sh before calling is:  1
time for aa.sh is 2016-07-15
count for aa.sh is 4
OPTIND for aa.sh after calling is:  5
OPTIND for bb.sh before calling is:  5
=time for bb.sh is 2016-07-15
count for bb.sh is 4
OPTIND for bb.sh after calling is:  5
```

Which is definitely not what we want.


We can now change bb.sh into the following to test it again.

```sh
echo "OPTIND for bb.sh before calling is: " $OPTIND

OPTIND=1

echo "we are setting the OPTIND to 1"
while getopts "t:c:" opt
do
    case "$opt" in
        t) time="${OPTARG}";;
        c) count="${OPTARG}";;
    esac
done

echo "time for bb.sh is $time"
echo "count for bb.sh is $count"

echo "OPTIND for bb.sh after calling is: " $OPTIND
```

and now "sh call.sh" will give out the following result,

```
OPTIND for aa.sh before calling is:  1
time for aa.sh is 2016-07-15
count for aa.sh is 4
OPTIND for aa.sh after calling is:  5
OPTIND for bb.sh before calling is:  5
we are setting the OPTIND to 1
time for bb.sh is 2016-07-20
count for bb.sh is 0
OPTIND for bb.sh after calling is:  5
```

What if we set the OPTIND to 3 now?

```sh
OPTIND for aa.sh before calling is:  1
time for aa.sh is 2016-07-15
count for aa.sh is 4
OPTIND for aa.sh after calling is:  5
OPTIND for bb.sh before calling is:  5
we are setting the OPTIND to 3
time for bb.sh is 2016-07-15
count for bb.sh is 0
OPTIND for bb.sh after calling is:  5
```

Now the count value is changed to 0, however time is still not changed.

How to understand this? First let us look at the definitions of $OPTIND and getopts

```
A getopts construct usually comes packaged in a while loop, which processes the options and
arguments one at a time, then increments the implicit $OPTIND variable to point to the next.
```

In a while loop contaning getopts, getopts will use $OPTIND to find the arguments. if we call the script using "dot" which is the same as using "source", $OPTIND will be global and available to the next script using getopts, and the next script will then can not find the right argument using $OPTIND now. 

The solution here is, we can reset $OPTIND to 1 or we can call the script using "sh" rather than "."
