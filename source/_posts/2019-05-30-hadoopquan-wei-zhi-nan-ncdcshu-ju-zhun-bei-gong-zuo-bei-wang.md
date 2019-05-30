---
layout: post
title: "Hadoop权威指南ncdc数据准备工作备忘"
date: 2019-05-30 09:23:39 +0800
comments: true
categories: BigData
---
<Hadoop: The Definitive Guide, Fourth Edition> <http://hadoopbook.com> 是本好书, 书中的例子用到了ncdc<ftp://ftp.ncdc.noaa.gov/pub/data/gsod/>的数据，这个也是非常赞的。我们知道统计学大师Fisher当年就是在气象工作站，研究气象数据很多年，后来在统计学上面做出了卓越的成就。气象数据纷繁复杂，通过实际的气象数据来阅读这本书，会教会读者在真实的情况下，如何面对数据，这个要比用一些dummy数据做演示，效果好太多.

官网github上面的数据很少<https://github.com/tomwhite/hadoop-book/tree/master/input/ncdc/all>. 我们自己从上面的ncdc的链接中去下载，我们下载tar文件. 具体也可以参考这篇文章<https://blog.csdn.net/mrcharles/article/details/50442367>

```sh
#!/bin/bash

#这里cd到你想下载到的目录, 每个文件的格式如下所示gsod_1901.tar, 发现tar文件竟然只有从1930年才不是空文件
cdir="$(cd `dirname $0`; pwd)"

for i in $(seq 1930 1960)
do
    wget --execute robots=off —accept=tar -r -np -nH --cut-dirs=4 - R index.html* ftp://ftp.ncdc.noaa.gov/pub/data/gsod/$i/
    done
```

下载好了之后，我们把这些1930/gsod_1930.tar 之类的文件，重新命令为1930/1930.tar, 然后把所有的文件都放到一个本地的目录，起名叫gsod， 现在gsod目录里都是1930/1930.tar这样的文件了.

接下来我们在hdfs上创建目录，

```sh
hdfs dfs -mkdir /GSOD /GSOD_ALL
```

然后将本地的gsod文件夹里的文件都上传到/GSOD/里面去

```sh
hdfs dfs -put gsod/* /GSOD/
```

这个过程在我的本机上，先是出现了namenode找不到的问题，然后又出现了namenode in safemode，创建不了的问题, 解决办法是

```sh
stop-all.sh
hdfs namenode -format
start-all.sh
hadoop dfsadmin -safemode leave
```

然后重新执行

```sh
hdfs dfs -put gsod/* /GSOD/
```

接下来我们要做的就是在hadoop上处理这些数据了. 首先创建generate_input_list.sh来生成MR的input文件:

```sh
#!/bin/bash

a=$1
rm -rf ncdc_files.txt
hdfs dfs -rm /ncdc_files.txt

while [ $a -le $2 ]
do
        filename="/GSOD/${a}/${a}.tar"
        echo "$filename" >> ncdc_files.txt
        a=`expr $a + 1`
done

hdfs dfs -put ncdc_files.txt /
```

ncdc_files.txt中的每一行就是``/GSOD/1950/1950.tar``这样的数据.

然后我们来产生文件:

```sh
sh generate_input_list.sh 1901 1956
```

接下来我们来创建load_ncdc_map.sh脚本，在MapReduce的Streaming上正常运行

```sh
#!/bin/bash

read offset hdfs_file
echo -e "$offset\t$hdfs_file"

# Retrieve file from HDFS to local disk
echo "reporter:status:Retrieving $hdfs_file" >&2
/Users/sun1/repo/hadoop-3.1.2/bin/hdfs dfs -get $hdfs_file .
# Create local directory
target=`basename $hdfs_file .tar`
mkdir $target

echo "reporter:status:Un-tarring $hdfs_file to $target" >&2
tar xf `basename $hdfs_file` -C $target
# Unzip each station file and concat into one file
echo "reporter:status:Un-gzipping $target" >&2
for file in $target/*
do
        gunzip -c $file >> $target.all
        echo "reporter:status:Processed $file" >&2
done
# Put gzipped version into HDFS
echo "reporter:status:Gzipping $target and putting in HDFS" >&2
gzip -c $target.all | /Users/sun1/repo/hadoop-3.1.2/bin/hdfs  dfs -put - /GSOD_ALL/$target.gz
rm `basename $hdfs_file`
rm -r $target
rm $target.all
```

然后我们可以使用如下的方式来调用这个shell脚本了:

```sh
#!/bin/bash

hadoop jar ${HADOOP_HOME}/share/hadoop/tools/lib/hadoop-streaming-3.1.2.jar \
    -D mapreduce.job.reduces=0 \
    -D mapreduce.map.speculative=false \
    -D mapreduce.task.timeout=12000000 \
    -inputformat org.apache.hadoop.mapred.lib.NLineInputFormat \
    -input /ncdc_files.txt \
    -output /output/gsod \
    -mapper load_ncdc_map.sh \
    -file load_ncdc_map.sh
```

最后运行完了，我们可以check下目标文件是否生成

```sh
hdfs dfs -ls /GSOD_ALL
```

以及检查输出的结果

```sh
hdfs dfs -cat /output/gsod/part-00053
```

