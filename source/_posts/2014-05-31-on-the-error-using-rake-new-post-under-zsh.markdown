---
layout: post
title: "ZSH下使用rake new_post报错"
date: 2014-05-31 17:48:54 +0800
comments: true
categories: Blog
---
When I issue the command "rake new_post[]" using the zsh, I got the error telling me that "no matches found". I googled, it said if using "noglob rake" rather than simply "rake", this problem will be solved. But in my case, it does not work. 

My expedient solution here is, issuing the followng command:   

```
rake "new_post[on the error using rake new_post under zsh]"
```   

rather than in the normal way:   

```
rake new_post["on the error using rake new_post under zsh"]
```  

It works in my case, but it is not a nice solution for sure.