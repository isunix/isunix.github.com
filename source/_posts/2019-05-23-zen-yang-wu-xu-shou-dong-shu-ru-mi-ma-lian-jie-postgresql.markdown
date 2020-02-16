---
layout: post
title: "怎样无需手动输入密码连接PostgreSQL"
date: 2019-05-23 08:44:13 +0800
comments: true
categories: Linux&Mac
---
我们要想不每次手动输入密码来连接PostgreSQL, 可以在home目录创建一个pgpass文件```touch ~/.pgpass```.
然后在里面输入如下的信息```$host:$port:$db:$user:$password```.
这里的每个变量实际过程中替换成真实的值.
然后我们就可以使用如下的方式来进行psql的连接了```psql -h $host -p $port -U $user -d $db```.
同理，这里的每个变量实际过程中替换成真实的值.


