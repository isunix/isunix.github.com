---
layout: post
title: "JS中根据某个key来给object排序"
date: 2016-03-09 09:41:03 +0800
comments: true
categories: Javascript
---
I have something like the following,

```js
var sophos = {name: "aa", time:"2016/03/02 01:12"};
var mcafee = {name: "bb", time:"2016/03/03 01:12"};
var trend = {name: "cc", time:"2016/03/04 01:12"};
```

and I want to find out the one with the earliest time, in the above code, it is "2016/03/02 01:12", and the corresponding item is "sophos", here is the realization is js code.

```js
var sophos = {name: "aa", time:"2016/03/02 01:12"};
var mcafee = {name: "bb", time:"2016/03/03 01:12"};
var trend = {name: "cc", time:"2016/03/04 01:12"};

var obj = [sophos, mcafee, trend];

function compare(a, b){
    if (a.time < b.time){
        return -1;
    }
    else if (a.time > b.time){
        return 1;
    }
    else {
        return 0;
    }
}

var result = obj.sort(compare);
console.log(result);
```