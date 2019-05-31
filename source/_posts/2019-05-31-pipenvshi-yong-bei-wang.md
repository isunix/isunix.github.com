---
layout: post
title: "pipenv使用备忘"
date: 2019-05-31 08:22:14 +0800
comments: true
categories: Python
---

我在某个python环境下有很多包，我们使用如下的命令把这些包给输出到requirements.txt里去

```sh
pip freeze > requirements.txt
```

然后我们使用pipenv来创建一个虚拟环境

```sh
mkdir xxx && mv requirements.txt xxx && cd xxx
pipenv --python 3.6
pipenv shell
pipenv install --dev
```

如果我们想删除创建的virtualenv, 可以

```sh
pipenv --rm
```

也可以到``~/.local/share/virtualenvs``下面去手动删除.



