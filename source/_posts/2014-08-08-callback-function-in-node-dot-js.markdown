---
layout: post
title: "callback function in node.js"
date: 2014-08-08 16:03:41 +0800
comments: true
categories: Node.js
---
Asynchronous IO in Node.js is very hard to understand. Here is one example from the book "Node.js开发指南".  

```js 

function readFileCallBack(err, data) {
  if (err) {
    console.error(err);
  } else {
    console.log(data);
  }
}

var fs = require('fs');
fs.readFile('file.txt', 'utf-8', readFileCallBack);
console.log('end.');  

```  

When fs.readFile is called, it just sents the asynchronous I/O to the operating system, then it comes back and executes the statements following it. After that, it enters into the event loop to listen on the event. When fs accepts the event finished by the I/O request, the event loop will call the callback function to finish the following work.  

Thus in this case, we will see the "end." first and then the contents of the file.txt.   

To understand how it works, it may help for us to get a basic knowledge of what is event. 

Take the following code as an example.    


```js  
     
var EventEmitter = require('events').EventEmitter;
var event = new EventEmitter();

event.on('some_event', function(){
  console.log('some_event occured.');
});

setTimeout(function () {
  event.emit('some_event');
}, 1000);
```  

We will see that "some_event occurred" appeares on the console. It is because event object registes a listener on the event some_event, we sent to "event" object the event some_event after a second(1000 ms) through setTimeout, it then will call the listener on some_event and the function is executed.   

Node.js 程序由事件循环开始，到事件循环结束，所有的逻辑都是事件的回调函数，所以 Node.js 始终在事件循环中，程序入口就是事件循环第一个事件的回调函数。事件的回调函数在执行的过程中，可能会发出 I/O 请求或直接发射（emit）事件，执行完毕后再返回事件循环，事件循环会检查事件队列中有没有未处理的事件，直到程序结束。

与其他语言不同的是，Node.js 没有显式的事件循环，类似 Ruby 的 EventMachine::run()的函数在 Node.js 中是不存在的。Node.js 的事件循环对开发者不可见，由 libev 库实现。libev支持多种类型的事件，如 ev_io、ev_timer、ev_signal、ev_idle 等，在 Node.js 中均被EventEmitter 封装。libev 事件循环的每一次迭代，在 Node.js 中就是一次 Tick，libev 不断检查是否有活动的、可供检测的事件监听器，直到检测不到时才退出事件循环，进程结束。






































