---
layout: post
title: "使用rpm安装crontab命令备忘"
date: 2019-05-22 16:36:21 +0800
comments: true
categories: Linux&Mac
---
我这边有台ec2, 但是在yum update的时候，总是报错说依赖冲突，后来处理这个问题的时候，过于激进，导致yum不可以用了, 最后把rpm也删了

参考这篇文章
<https://blog.seosiwei.com/detail/27>
里的方法2，把rpm和yum都删了然后重装了, 软件下载链接是
<http://mirrors.ustc.edu.cn/centos/6/os/x86_64/Packages/>

安装好了之后，发现yum还是不能用，总是报错

```
liblzma.so.0: cannot open shared object file: No such file or directory
```
之类的信息

无可奈何，只好使用rpm了, 我这边需要使用crontab，于是从上面的软件库中下载了

```
cronie-1.4.4-16.el6_8.2.x86_64.rpm``` 和 ```crontabs-1.10-33.el6.noarch.rpm
```

然后执行如下的命令来安装

```
rpm -Uvh --replacepkgs --nodeps --force cron*.rpm
```

然后报各种依赖找不到的错误, 比如

```
librpmio.so.3 not found
```
之类的

好在我们有别的ec2，我们可以去这个另外的ec2上找对应的依赖，然后copy到这个我们出问题的机器上

```
find / -name librpm.so.3 -type f
```

然后发现在/usr/lib64中，librpm.so.3是个软连接，指向/usr/lib64中的librpm.so.3.2.2, 我们把librpm.so.3.2.2copy到我们出问题的机器的/usr/lib64里，然后参照
<http://isunix.github.io/blog/2019/05/22/linuxming-ling-lnde-shi-yong-bei-wang/>
中的方式来做个软连接

仿照这个方式，如果还有问题，重复找依赖-copy-做软连接的过程

最后再执行

```
rpm -Uvh --replacepkgs --nodeps --force cron*.rpm
```
crontab命令成功安装了.
