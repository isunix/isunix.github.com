---
layout: post
title: "Presto问题debug"
date: 2019-06-04 10:27:51 +0800
comments: true
categories: BigData
---
我们在执行presto-cli命名的时候，可以使用如下的方式 ``presto-cli --catalog hive --schema $schema --output-format CSV_HEADER --server $ip:$port --debug``

这样就会打印出诊断信息出来.

我们使用如下的命令看下presto-server的状态 ``initctl list | grep -i presto``

``sudo stop presto-server`` 这样来关闭 presto-server； ``sudo start presto-server`` 这样来开启.

如果想要看查看presto的log，可以去 ``/var/log/presto``, 对于debug非常有用.

