---
layout: post
title: "alternative way to bypass problems met when rake new_post"
date: 2015-06-01 11:06:22 +0800
comments: true
categories: Blog	
---
I met errors while I am issuing the command "rake new_post" add generate a new post. Here is an alternative way to generate new post:

```ruby
bundle exec rake "new_post[alternative way to bypass problems met when rake new_post]"
```

and then we can use the "Mou" app to open the page:

```ruby
open -a Mou source/_posts/2015-06-01-alternative-way-to-bypass-problems-met-when-rake-new-post.markdown
```
