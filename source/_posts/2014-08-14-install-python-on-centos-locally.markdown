---
layout: post
title: "install python on centos locally"
date: 2014-08-14 12:25:15 +0800
comments: true
categories: Python
---
This post depicts how to install Python on the CentOS in your local dir.  

1.First show the python2.x version.

```py
wget http://python.org/ftp/python/2.7.6/Python-2.7.6.tar.xz   
tar -zxvf Python-2.7.6.tar.xz  
cd Python-2.7.6  
./configure --prefix=/home/sun/local --enable-unicode=ucs4 --enable-shared LDFLAGS="-Wl,-rpath /home/sun/local/lib"  
make && make altinstall

wget https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py  
python ez_setup.py
easy_install-2.7 pip
pip2.7 install [packagename]   
(pip defaults to pip2.7)
```

2.Now the python3.x version

```py
wget http://python.org/ftp/python/3.4.1/Python-3.4.1.tar.xz
tar xf Python-3.4.1.tar.xz
cd Python-3.4.1
./configure --prefix=/hom/sun/local --enable-shared LDFLAGS="-Wl,-rpath /home/sun/local/lib"
make && make altinstall  

wget https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py  
mv python3.4 python3
python3 ez_setup.py
easy_install-3.4 pip
pip3 install [packagename]   

```  

If you want to install the package used by python3, you need to using the command "pip3 install [packagename]", otherwise just "pip install [packagename]"
