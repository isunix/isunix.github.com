---
layout: post
title: "有用的JS代码片段"
date: 2014-08-31 17:47:03 +0800
comments: true
categories: Javascript
---
1.To sort an array from small to big nums, we can use the following method.

```js
function compare(num1, num2){
  return num1 - num2;
}

var nums = [3,1,2,100,4,200];
nums.sort(compare);
print(nums);
```

2.reduce, every, some, forEach迭代器方法

3.map will give out a new array:

```js
function first(word){
  return word[0];
}

var words = ["for", "your", "info"];
var acronym = words.map(first);
print(acronym.join(""));
//fyi

//print(acronym);
//f,y,i

```
note how we used join to avoid the ","

4.filter

Filter is quite similar to "every", it accept a function whose return value is boolean. In contrast to "every", when filter(func) evaluated to true, it does not retrun "true", it returns a new array, whose item is the those items in the original way after beed passed to the funcition.

```js
function passing(num) {
   return num >= 60;
}

var grades = [];
for (var i = 0; i < 20; ++i) {
   grades[i] = Math.floor(Math.random() * 101);
}
var passGrades = grades.filter(passing);
print(grades);
print(passGrades);
```

5.the following code shows how to get a studetnt's average score and how to get a discipline's averge score.

```js
//discipline's average score

var grades = [[89, 77, 78],[76, 82, 81],[91, 94, 89]];
var total = 0;
var average = 0.0;
for (var col = 0; col < grades.length; ++col) {
   for (var row = 0; row < grades[col].length; ++row) {
      total += grades[row][col];
   }


   average = total / grades[col].length;
   print("Test " + parseInt(col+1) + " average: " +
         average.toFixed(2));
   total = 0;
   average = 0.0;
}

//a student's average score

var grades = [[89, 77, 78],[76, 82, 81],[91, 94, 89]];
var total = 0;
var average = 0.0;
for (var row = 0; row < grades.length; ++row) {
   for (var col = 0; col < grades[row].length; ++col) {
      total += grades[row][col];
   }
   average = total / grades[row].length;
   print("Student " + parseInt(row+1) + " average: " +
         average.toFixed(2));
   total = 0;
   average = 0.0;
}
```
