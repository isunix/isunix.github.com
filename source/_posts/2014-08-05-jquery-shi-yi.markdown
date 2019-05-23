---
layout: post
title: "jquery 拾遗"
date: 2014-08-05 11:18:49 +0800
comments: true
categories: Javascript
---
This blog post is about some of the usages of jQuery while I am learning and using jQuery. I keep a note of it so that I can pick it up conveniently later.

1. append a paragraph to the front of your body.

```js

var para = $("<p>", {"text": "I'm a new paragraph!", "css":{"background":"yellow"}});
$("body").prepend(para)

```

and also we can do it using the "prepentTo" method.

```js

$("<p>", {"text": "I'm a new people!", "css":{"background":"red"}}).prependTo("body");

```

If we want to insert before/after an element, we can use the following method.

```js

$("<p>", {"text": "a new paragraph."}).insertAfter("p.foo");

```

For the "wrap" method, it is like this:

```js

$("span").wrap("<strong />");

```
This will wrap all "span"" tag with "strong" tag. Or we can have the nested tags inside "wrap":

```js

$("span").wrap("<strong><em></em></strong>");

```

2. We can also use callback function to do some selective adding.

```js

$("span").wrap(function(){return $(this).is(".foo") ? "<strong>" : "<em>"});

```

3. to get the last id attributes of a paragraph:

```js

$("p:eq(3)").attr("id");

```
and to modify its id to "bar", we can do this:

```js

$("#bar").attr("id", "bat")

```

4. if you want to remove an attribute from an element, we can use the "removeAttr" method.

```js

$(":checkbox").removeAttr("disabled");

```

5. text() can just act on "text", while html() can act on html contents.

6. .val() is used to get the value or content of a form element, like:

```js

$(":submit").val();

```

or

```js

$(":submit").val("Sign IN");

```

7. .addClass(), .removeClass(), .toggleClass() are also 3 often used methods.

8. .map() and .each(), .show() and .hide(), .fadeIn(), .fadeOut(), .fadeTo() , these are common methods.
