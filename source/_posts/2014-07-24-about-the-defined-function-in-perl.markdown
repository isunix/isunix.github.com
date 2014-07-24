---
layout: post
title: "about the defined function in perl"
date: 2014-07-24 16:09:53 +0800
comments: true
categories: Perl
---
在"perl for dummies" 这本书中有段很精彩的关于defined 函数的说明。现在记录如下:    

在perl中构建语句的一个基本规则是: 使用变量前应该在赋值语句的右边定义它们，这样做可以防止perl给未定义的变量插入默认值.  

未定义的变量的存在是有意义的。照搬书中的例子，如果试图从空列表中提取数据， pop函数就会返回一个未定义的值。让pop函数返回未定义的值比返回假值要好，因为'false'可能就是列表中的某个元素。  

那么我们怎么去判断一个函数是否返回未定义的值呢？ 这里"defined" 就派上用场了。该函数会作用于一个变量或者表达式。如果这个被作用的对象已被定义，defined函数就会返回真， 否则就会返回假。 通常会跟着if或者unless来使用的。  

```perl
unless (defined($Yummy = pop(@Bonbons))){
	print "there are no more bonbos left.";
}  

```  
如果@Bonbons这个列表是空的， defined函数就会返回假值，就会执行print语句，这个时候$Yummy变量将包含一个未定义的值。   


