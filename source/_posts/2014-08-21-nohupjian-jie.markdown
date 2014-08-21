---
layout: post
title: "nohup简介"
date: 2014-08-21 15:45:34 +0800
comments: true
categories: Python
---
我把这个东西放到Python的category里来，是因为我在写Flask的web应用的时候，遇到部署的问题，需要用到一个工具， 可以一直让这个web进程去运行。土鳖的我还以为这得用到cronjob， 其实用个工具可以帮我们完成这样的一个任务的， 这就是这篇post所要介绍的"nohup"

比如说我现在在一个叫server.sh的文件中写入了如下的内容来run一个web server:  

```sh
gunicorn -w 4 -b 0.0.0.0:1234 myapp:app
```  

首先这个Flask web apppication, 不同的框架使用gunicorn大同小异。然后使用的是gunicorn这个http server. 具体的关于gunicorn的知识可以自己去查下。只是有点是：你得先安装下的:  

```py
pip install gunicorn
```  

Here the "-w" args means worker, namely 4 processes here.   

For my application, if I want to use nohup, I will have to issue the following command. 

```sh
nohup ./server.sh &
```

Nohuo will create a nohup.out file in the directory where you run the command. 

nohup 只不过是让进程脱离父进程, 这样即使父进程死掉，它也还在运行。

Thus if we want to use "jobs" to see process, we will not be able to see it. we can use the "ps a" command line to see the the process.  

使用 fg %jobnumber　会将任务拿到前台执行，拿到前台后如果要关闭这个任务按Ctrl+c组合键即可，但如果要暂停这个任务可以按Ctrl+z组合键这时就会将任务置于暂停状态。




