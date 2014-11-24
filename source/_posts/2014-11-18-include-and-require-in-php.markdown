---
layout: post
title: "include and require in PHP"
date: 2014-11-18 13:42:05 +0800
comments: true
categories: PHP
---

For a person who has experience in programming PHP, he should have heard the concept of "include", "include_once", "require", "require_once". We will give a little deailed info here.

1.include_once

```
The include_once statement includes and evaluates the specified file during the execution of the script. This is a behavior similar to the include statement, with the only difference being that if the code from a file has already been included, it will not be included again. As the name suggests, it will be included just once.

include_once may be used in cases where the same file might be included and evaluated more than once during a particular execution of a script, so in this case it may help avoid problems such as function redefinitions, variable value reassignments, etc.
```  

2.require and include

```
the differences between require and include are:  

当要包含的文件不存在时,include产生一个警告(Warning)该语句后面的程序会继续执行；而require则导致一个致命错误（Fatal error),程序就此终止。

include_once和require_once
应该用于在脚本执行期间同一个文件有可能被包含超过一次的情况下, 想确保它只被包含一次以避免函数重定义, 变量重新赋值等问题.
  
*.incluce在用到时加载，这个函式一般是放在流程控制的处理区段中
*.require在一开始就加载，这个函式通常放在PHP程式的最前面
*._once后缀表示已加载的不加载
```  
