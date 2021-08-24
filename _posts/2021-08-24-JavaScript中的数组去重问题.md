---
title: JavaScript中的数组去重问题
tags: 学习记录
---

# JavaScript中的数组去重问题

## 问题

> JavaScript中数组的去重方法
>
> 例：
>
> arr = [1, 2, 3, 2, 1, 3, 2, 1, 3, 4, 2, 5];
>
> 在去重以后，会得到结果
>
> arr = [1, 2, 3, 4, 5]

## 解决方法
### 方法一：双重循环（利用splice方法）
```javascript
var arr = [1, 2, 3, 2, 1, 3, 2, 1, 3, 4, 2, 5];

for (let i = 0; i < arr.length; i++) {
    for (var j = i + 1; j < arr.length; j++) {
        // 使用splice进行去重 splice(pos,num) pos:要删除的元素所在的位置 num:从第一个要删除的元素开始，删除的数量
        if(arr[i] == arr[j]){
            arr.splice(j,1); //在index为j时，发现重复元素，因此把这个元素删掉
            j--; 
            // 此处为易错点，需要把index-1
            //如果j元素的下一个位置仍然是该重复值，由于j位置元素被删掉了，会往前移动，导致未发现该重复值
        }
    }
}

console.log(arr); //[ 1, 2, 3, 4, 5 ]
```

### 方法二：利用Set去重
Set（集合）中的元素不可重复，所以如果能把数组转换成集合，就可以实现去重
```javascript
var arr = [1, 2, 3, 2, 1, 3, 2, 1, 3, 4, 2, 5];
var set1 = new Set(arr);
console.log(set1); // Set(5) { 1, 2, 3, 4, 5 }
```
### 方法三：利用indexOf/includes方法

> indexOf方法：返回数组中可以找到给定元素的第一个索引，不存在则返回-1

那么可以利用该方法，如果newArr中不存在该元素，则会返回-1，可以将其加入newArr，否则不加入。
```javascript
var oddArr = [1, 2, 3, 2, 1, 3, 2, 1, 3, 4, 2, 5];
var newArr = [];
for (let i = 0; i < oddArr.length; i++) {
    if (newArr.indexOf(oddArr[i]) == -1) {
    // if (!newArr.includes(oddArr[i])) {
        newArr.push(oddArr[i]);
    }
}

console.log(newArr); // [ 1, 2, 3, 4, 5 ]
```

> includes方法与indexOf方法类似，包含则返回true，不包含则返回false。



> 区别：indexOf不会对NaN进行去重，但是includes会。
>
> var oddArr = [1,2,3,1,2,3,NaN,NaN,NaN];
>
> indexOf方法的结果：[ 1, 2, 3, NaN, NaN, NaN ]
>
> includes方法的结果：[ 1, 2, 3, NaN ]

### 方法四：使用sort()排序方法

<!--more--> 

---

2021年8月24日

