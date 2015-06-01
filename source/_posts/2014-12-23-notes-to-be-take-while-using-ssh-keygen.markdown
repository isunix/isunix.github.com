---
layout: post
title: "notes to be take while using ssh-keygen"
date: 2014-12-23 20:18:10 +0800
comments: true
categories: Perl
---
I encoutered some problems while I was using ssh-keygen, it turns out to be originating from privileges setting up.

The following way turns out to be working.

1.Do not set up your home directory to be "777", it will not work. I set it to be "755"

```sh
chmod 755 /home/stsun
```

2.

```sh
chmod 600 authorized_keys 
```

3.

```sh
chmod 700 .ssh
```

And then it works well.