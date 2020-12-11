---
layout: post
title: "Pandas使用tips集锦"
date: 2020-12-11 09:18:43 +0800
comments: true
categories: Data&ML&AI
---
1. 替换字符

```py
auto['horsepower'] = auto['horsepower'].replace('?',np.nan)
```

2. 删除空值

```py
auto = auto.dropna()
```

3. 改变字段类型

```py
auto['horsepower'] = auto['horsepower'].astype('int')
```

4. 按照某一个字段排序

```py
auto = auto.sort_values(by = ['horsepower'],ascending = True, axis = 0)
```
