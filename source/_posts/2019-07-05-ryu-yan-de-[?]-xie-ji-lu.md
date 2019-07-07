---
layout: post
title: "R语言的一些记录"
date: 2019-07-05 08:00:01 +0800
comments: true
categories: Data&ML&AI
---
在R语言中，如果我们有一个`vector` 叫 `x`, `x` 的值中有 `NA`，如果我们想要过滤掉 `x` 中的 `NA`, 并把过滤后的结果，赋值给变量 `y`， 可以如下操作:

```r
y <- x[!is.na(x)]
```

如果我们再想找出 `y` 中元素大于0的元素，可以如下操作L:

```r
y[y > 0]
```

以上两步合在一起，可以如下操作:

```r
x[!is.na(x) & x > 0]
```

如果我们直接使用 `x[x > 0]` 是不行的，会得到如下的包含`NA` 值的一个 `vector`:

```
 NA        NA 0.3488261        NA 2.4099262        NA        NA        NA        NA        NA 0.4626879
```

创建一个4行5列的`matrix`，包含的数值是从1到20，

```r
my_matrix <- matrix(data=1:20, nrow = 4, ncol = 5)
```

如果我想给这个`matrix`的每行添加一列，作为名字，可以采用如下的方式

```r
patients <- c("Bill", "Gina", "Kelly", "Sean")
cbind(patients, my_matrix)
```

但是上面这种方式，会导致`implicit coercion`, 把数字变成字符，为了解决这个问题，我们可以使用如下的方式

```r
my_data <- data.frame(patients, my_matrix)
```

如果我们再想给每个列增加一个`name`, 可以使用如下的方式:

```r
cnames <- c("patient", "age", "weight", "bp", "rating", "test")
colnames(my_data) <- cnames
```

如果我们想要获取当前的工作目录,

```r
getwd()
```

如果我们想要切换到另外一个目录，可以

```r
setwd("~/data/ISLR")
```