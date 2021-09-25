---
layout: post
title: "PHP中添加jquery文件的几种方法"
date: 2014-08-01 15:03:11 +0800
comments: true
categories: PHP
---
The following are several addtional ways to include a jquery file in your php script.  

```js
<script type="text/javascript" src="js/jquery-1.11.1.min.js"></script>
```  
or  

```js
<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js">
</script>
```   
or  

```js
<script type="text/javascript" src="http://www.google.com/jsapi"> </script>

<script type="text/javascript">
	google.load("jquery", "1.7.1");
</script> 
```

