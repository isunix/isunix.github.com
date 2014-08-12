---
layout: post
title: "notes on the use of module in node.js"
date: 2014-08-08 17:11:27 +0800
comments: true
categories: Node.js
---
1. require 不会重复加载模块，也就是说无论调用多少次 require，获得的模块都是同一个。  

2. Node.js 提供了 exports 和 require 两个对象，其中 exports 是模块公开的接口，require 用于从外部获取一个模块的接口，即所获取模块的 exports 对象。   
3. exports 本身仅仅是一个普通的空对象，即 {}，它专门用来声明接口，本质上是通过它为模块闭包的内部建立了一个有限的访问接口.   
4. Node.js 在调用某个包时，会首先检查包中 package.json 文件的 main 字段，将其作为包的接口模块，如果 package.json 或 main 字段不存在，会尝试寻找 index.js 或 index.node 作为包的接口。5. following the following steps to create and publish a module. 

* mkdir stsunmodule  
* cd stsunmodule  
* npm init  (then answer all the questions as been prompted)    
* touch index.js   
* npm adduser  
* npm whoami  (use this command to test if your account is created successfully)   
* npm publish   
then you can go to the site "https://search.npmjs.org" to check if your module is published successfully.  
You can also use "npm unpublish" to unpublish your module.  