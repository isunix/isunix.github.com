---
layout: post
title: "Notes On Flask"
date: 2014-08-27 12:10:36 +0800
comments: true
categories: Python
---
I have been learning Flask for quite a while. This is a note to keep down of all those snippets and notes I have learnt and hope to keep it as a reminder.  

1.if you want to get the browser info, use the following code:  

```py
from flask import request@app.route('/')def index():	user_agent = request.headers.get('User-Agent')	return '<p>Your browser is %s</p>' % user_agent
```  

2.There are two contexts in Flask: the application context and the request context.  

3.before_first_request: Register a function to run before the first request ishandled.  
4.before_request: Register a function to run before each request.  
5.after_request: Register a function to run after each request, if no unhandled exceptions occurred.  
6.teardown_request: Register a function to run after each request, even if unhandledexceptions occurred.