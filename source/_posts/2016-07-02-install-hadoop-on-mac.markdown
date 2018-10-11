---
layout: post
title: "install hadoop on mac"
date: 2016-07-02 16:16:15 +0800
comments: true
categories: Hadoop
---
这篇blog是关于如何在mac上安装hadoop的。 参考书目是《hadoop 核心技术》 by 翟周伟， 还有这篇博文， http://dongfeiwww.com/hadoop/2014/09/05/hadoop-on-mac/。

要要注意的点是， 如果是安装hadoop在／usr/local这种路径下， 最后跑start-dfs.sh这种脚本的时候， 是需要sudo权限的， 所以可以按照“核心技术”这本书来， 把hadoop解压到本地一个不需要sudo权限去访问执行的地方。

第二点就是start-all.sh这个脚本被deprecated的了， 推荐使用的是，start-dfs.sh and start-yarn.sh这种单独的脚本。

第三就是运行下ssh localhost看能不能连上。

最后， 配置成功后能从web页面访问到的端口有

```html
http://localhost:50090/status.html      (Secondary NameNode status)
http://localhost:50070/dfshealth.html#tab-overview    (hdfs status)
```

