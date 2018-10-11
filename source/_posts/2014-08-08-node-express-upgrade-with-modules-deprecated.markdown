---
layout: post
title: "node express upgrade with modules deprecated"
date: 2014-08-08 15:17:47 +0800
comments: true
categories: Node.js
---
The "express" web application framework for node updates termly. Thus some of the apis may not be usable after a while. Here below are some of the apis deprecated between version2.5.2 and version4.8.2.   

```js

`express.createServer()` - it has been deprecated for a long time. Use `express()` 

deprecate `connect.createServer()` -- use `connect()` instead

deprecate `.createServer()` & remove old stale examples

Added `express.createServer()` for BC

Fixed for middleware stacked via `createServer()`

previously the `foo` middleware passed to `createServer(foo)` 

express.bodyParser() will have to be installed separately.

```