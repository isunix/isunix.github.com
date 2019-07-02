---
layout: post
title: "用Python来发送markdown格式的邮件"
date: 2019-07-02 15:19:06 +0800
comments: true
categories: Fun
---
## https://github.com/yejianye/mdmail

mdmail， 这个是一个支持用 markdown 格式来发送邮件的工具.

```py
import mdmail

email="""
# Sample Email
- Python is awesome
- Markdown is cool
"""

mdmail.send(email, subject='Sample Email Mdmail',
            from_email='mypeacelover@163.com', to_email='mypeacelover@163.com')
```

很好用, 汪汪.
