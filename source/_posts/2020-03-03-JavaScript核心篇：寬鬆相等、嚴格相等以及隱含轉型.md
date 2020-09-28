---
title: JavaScript核心篇：寬鬆相等、嚴格相等以及隱含轉型
date: 2020-03-03 13:07:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 寬鬆相等、嚴格相等以及隱含轉型

> 「== 允許在比較中強制轉型，=== 不允許。」

## 嚴格相等

嚴格相等必須**值**、**型別**都要相同才會回傳 true。

![嚴格比較](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Ftruthy%26falsy%E5%9A%B4%E6%A0%BC%E6%AF%94%E8%BC%83.jpg?alt=media&token=eba46e48-5fd1-425e-aeab-cdc081700256)


```
console.log(1 === '1'); // false  // '1'是字串
console.log(1 === 1); // true
console.log(1 !== '1'); // true


// 不過嚴格相等有兩個例外

console.log(NaN === NaN); // false
console.log(+0 === -0); //true
```

## 寬鬆相等

寬鬆等於只要值相等就會回傳 true，這裡說的值包含**字串**、**布林**轉化過來的值。

![寬鬆比較](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Ftruthy%26falsy%E5%AF%AC%E9%AC%86%E6%AF%94%E8%BC%83.jpg?alt=media&token=cdc6fb06-3ea3-4897-bf58-6fbc83676b8e)

```
console.log(1 == '1'); // true
console.log(true == '1'); // true
console.log(false == '0'); // true
console.log(1 != '1'); //false

console.log(Number(!0)); // 1
console.log(1 == !0); // true
```

Null 跟 undefined 不能被轉化為數字型別。

## 物件與非物件比對

在物件與非物件比對的時候，是使用**包裹物件**來進行轉換。

```
console.log(Number([10])); // 10
console.log(10 == [10]); // true

console.log(String(['A'])); // 'A'
console.log('A' == ['A']);  // true
```


## 物件比對

物件經過隱含轉型後，會變成 [object Object]。

```
var a = {c: 5};
var b = {c: 5};

a < b; // false
a > b; // false
a == b; // false
```

object 指向的是記憶體位置，所以 a == b 時不會相等。

> [圖片取自](https://dorey.github.io/JavaScript-Equality-Table/)