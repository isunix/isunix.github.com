---
layout: post
title: "apache服务设置重定向地址"
date: 2014-11-24 14:31:59 +0800
comments: true
categories: Perl
---
While I was developing a dancer application, I usually open a new port, like goople.com:4001. Actually there is a better way to do this.

On our CentOS server, in the httpd.conf file, we include the following piece to it:

```html
Include etc/apache22/Includes/*.conf
```

If it is not already there.

Then in the dir,  /usr/local/etc/apache22/Includes, we will write our own configuration file.

Then we can make a file named sun.conf in the Includes dir and write to it something like this:

```html
Alias /~stsun /home/stsun/public_html

<Directory "/home/stsun/public_html">
	Options +Indexes FollowSymLinks
	AllowOverride All
	Order allow,deny
	Allow from all
</Directory>
```

Of course we have another way for this:

```html
NameVirtualHost *:8080
<VirtualHost *:8080>
    DocumentRoot "/Users/sun/w"
    <Directory "/Users/sun/w">
        DirectoryIndex index.html
        AddHandler cgi-script .py .pl
        AddType text/html .py .html .pl
        Options ExecCGI
        Order Allow,Deny
        AllowOverride All
        Allow from all
    </Directory>
</VirtualHost>
```