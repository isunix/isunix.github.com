---
layout: post
title: "beginning python study notes"
date: 2014-06-27 16:15:19 +0800
comments: true
categories: Python
---
1. input会假设用户的输入是合法的python表达式，而raw_input则不做这样的要求的。  
2. 在python中列表可以修改， 而元组则不能；会使用改变列表的常用method。   
3. 一般使用元组作为字典的建， 这种情况下，因为键不可修改，所以就不能够使用列表了。  
4. 列表的各个元素通过逗号分隔， 写在方括号中。   
5. 如果分片所得部包括序列结尾的元素， 那么，只需置空最后一个索引即可， 如numbers[-3:], 同样的方法也可以用于序列的开始的元素的。numbers[:3], 如果需要复制整个的序列，可以将两个索引都置空的: numbers[:]   
6. pop方法是唯一一既能修改列表又返回元素值的列表方法(除了None)。
7. （42，）这是只有一个元素的元组。  
8. strip方法返回去除两侧(不包括内部)空格的字符串；
9. 字典中的值并没有特殊的顺序，但是都存储在一个特定的键里， 键可以是数字， 字符串， 甚至是元组。  
10. range函数包含下限， 但是不包含上限。   
11. break会跳出循环， 而continue会结束当前的迭代然后跳到下一轮循环的开始的。  
12. 想要什么事情都不做， 使用pass就可以了。
13. 执行一个字符串的语句是exec， 如， exec “print ”hello world“   
14. eval会计算python表达式， 并且返回结果值。  
15. 并非所有的python函数都是有返回值的。
16. get used to "try except else clause".
17. try finally, finally 可以在可能的异常后面进行清理。   
18. sys这个模块能够让你访问与python解释器联系紧密的变量还有函数。
19. os模块为你提供了多个访问操作系统服务的功能。  
20. 关注fileinput这个模块。   
21. 关注time模块。
22. 关注re模块。
23. re.compile将正则表达式(以字符串书写的)转换为模式对象，可以实现更有效率的匹配。  
24. 关注getopt还有optparse这两个模块。  
25. dir(obj)会返回按字母顺序排序的属性名称列表。  
26. help(obj)会提供交互式帮助或者关于特定对象的交互帮助信息。   
27. python的open函数的第三个参数控制着文件的缓冲， 如果参数是0， I/O就是无缓冲的， 如果是1， I/O就是有缓冲的, 这就意味着python使用内存来代替硬盘， 让程序更快， 是有使用flush或者close的时候才会更新硬盘上的数据。大于1的数据代表缓冲区的大小，-1代表使用默认的缓冲区的大小。  
28. 关注urllib还有urllib2模块。   
29. 关注HTMLParser模块。  
30. 关注模块BeautifulSoup4
