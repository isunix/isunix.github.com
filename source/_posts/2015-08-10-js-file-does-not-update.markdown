---
layout: post
title: "js file does not update"
date: 2015-08-10 16:00:36 +0800
comments: true
categories: js
---
The problem is: I have to update a js file, say in the dir public_html/js/aa.js. also I have to upate it in another dir, like public_html2/js/aa.js

However aftering changing the file, one works the other still the same.

After exploring for a while, the solutiio is: just change the js file name and change the name where the file is used.

The problem was caused by cache. We can file more by looking at the page:

```
http://stackoverflow.com/questions/32414/how-can-i-force-clients-to-refresh-javascript-files
```