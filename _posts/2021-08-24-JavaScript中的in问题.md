---
title: JavaScript中in的问题
tags: 学习记录
---

# JavaScript中in的问题

## 一、问题起源

> JavaScript中数组的去重方法
>
> 例：
>
> arr = [1, 2, 3, 2, 1, 3, 2, 1, 3, 4, 2, 5];
>
> 在去重以后，会得到结果
>
> arr = [1, 2, 3, 4, 5]

一开始，在习惯性认知下，写出了这样的代码
```javascript
var arr1 = [1, 2, 3, 2, 1, 3, 4, 2, 5];
var arr2 = [];
for(let i = 0;i<arr1.length;i++){
    if(!(arr1[i] in arr2))
        arr2.push(arr1[i]);
}
console.log(arr2);
```

得到如下运行结果：

> [Running] node "c:\Users\hucon\Desktop\Code\array.js"
> [ 1, 2, 3, 3, 4, 5 ]
## 二、问题原因

为什么会发生这样的问题呢？原因如下：

当in的对象是**数组**时，in前面的的变量指的是**数组的索引值**，**而不是具体的元素**。

例如：
```javascript
var arr = ["a", "b", "c", 4, 5, 6];
console.log(1 in arr); // true
console.log("a" in arr); // false
console.log(6 in arr); // false 
```

> 1 in arr 的结果为true，并不是说arr数组中有"1"这个元素，而是说arr数组中index为1的位置有值（值为"b"）。
> “a" in arr 的结果为false，6 in arr的结果为false，就容易理解了。

## 三、补充
### 3.1 当in的对象是Object时，此时in前面的变量指的就是该对象是否有此属性
例如：
```javascript
var obj={
    a:"text1",
    b:"text2",
    c:"text3"
}
console.log("a" in obj); // true
console.log(1 in obj); // false
```
> "a" in obj 的结果为true，是因为obj对象中有名为a的属性
> 1 in obj 的结果为false，是因为obj对象中没有1这个属性

### 3.2 for…in 循环
在 for…in 循环中，in前面的变量代表的是索引值（在数组中）和属性名（在对象中）。
```javascript
var arr = ["a", "b", "c"];
for (var index in arr) {
    console.log(arr[index]);
}

var obj = {
    a: 'aaa',
    b: 'bbb',
    c: 'ccc'
}

for (var index in obj) {
    console.log(obj[index]);
}
```

### 附录
关于JavaScript中的数组去重问题，见此篇文章。


<!--more-->

---

2021年8月24日

