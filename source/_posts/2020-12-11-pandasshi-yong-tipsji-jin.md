---
layout: post
title: "Pandas使用tips集锦"
date: 2020-12-11 09:18:43 +0800
comments: true
categories: Data&ML&AI
---

### 1. 替换字符

```py
auto['horsepower'] = auto['horsepower'].replace('?',np.nan)
```

### 2. 删除空值

```py
auto = auto.dropna()
```

### 3. 改变字段类型

```py
auto['horsepower'] = auto['horsepower'].astype('int')
```

### 4. 按照某一个/多个字段排序

```py
auto = auto.sort_values(by = ['horsepower'],ascending = True, axis = 0)

boston.sort_values(by= ['CRIM','TAX','PTRATIO'],ascending=False).head().index
```

### 5. pandas设置索引

```py
college = college.set_index(['Unnamed: 0'], append=True, verify_integrity=True) college.rename_axis([None, 'Name'], inplace=True)
``` 

### 6. 对某一列进行判断并且置值

```py
college['Elite'] = np.where(college['Top10perc'] > 50,'Yes','No')
```

### 7. 对某一列的值进行计数

```py
college['Elite'].value_counts()
```

### 8. 对某一列的值进行筛选

```py
elite_colleges = college[college['Elite'] == 'Yes']
```

### 9. 对某一列的数值进行分桶操作

```py
college['Enroll'] = pd.cut(college['Enroll'], bins=3, labels = ['Low','Medium','High'])
```

### 10. 查看df中的各个字段的unique的数目和字段类型信息等

```py
auto.nunique()
auto.info()
auto['horsepower'].unique() # 看某一列的unique数目
```

### 11. 筛选单列和多列

```py
info['range'] = info['max'] - info['min'] 
info = info[['mean','range','std']]
```

### 12. 根据index筛选和删除多列

```py
info = auto.drop(auto.index[10:85]).describe().T
```

### 13. load数据并且指定列名

```py
boston = pd.DataFrame(load_boston().data,columns = load_boston().feature_names )
```

### 14. 通过iloc选取行和列

```py
corr_matrix = boston.corr() 
corr_matrix.iloc[1:,0].sort_values() 

# 选取所有行，和从第二列开始的所有列
data = data.iloc[:,1:]
```

## 参考链接

[pandas中关于set\_index和reset\_index的用法](https://blog.csdn.net/jingyi130705008/article/details/78162758
)