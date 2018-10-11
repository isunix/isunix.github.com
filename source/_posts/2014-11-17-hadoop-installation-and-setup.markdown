---
layout: post
title: "hadoop installation and setup"
date: 2014-11-17 17:23:12 +0800
comments: true
categories: ML
---
This is for setting  up hadoop on ubuntu. I am using hadoop version 2.5.1, so when I search on the internet, the result I get may not apply to the version I am using, thus I keep a note of the installation process in the hope that later reference will be easier.  

1.install java and set java home env variable. 

In the /etc/lib/jvm dir, make a soft link to the jdk dir their and renaming it ot "jdk" for short nanme.  and write to my .zshrc file the JAVA_HOME path variable. 

2.edit the hadoop-env.sh file in hadoop/etc/hadoop dir by setting the java home var.

3.edit the core-site.xml file in hadoop/etc/hadoop dir by setting the default hadoop config which you can search by yourself.

4.edit the hdfs-site.xml file in hadoop/etc/hadoop dir by setting the default fs config which you can search by yourself.

5.edit the map-red.site.xml file in hadoop/etc/hadoop dir by setting the default fs config which you can search by yourself.  

6.format hdfs by issuing the following command:  

```sh
./bin/hadoop namenode -format
```

7.start services by executing the scripts in the sbin dir.

```sh
./start-yarn.sh
```
(It is not in the bin dir as is shown in most blogs.)