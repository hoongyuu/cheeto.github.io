---
title: JavaScript核心篇：優先性、相依性
date: 2020-03-02 21:02:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 優先性及相依性

## 優先性

優先序較高的運算子會成為優先序較低的運算子的運算元。例:乘除的符號優先性大於加減，所以會先乘除後加減。

## 相依性

相依性決定運算方向。例:加減乘除都是由左至右、等號則是由右至左。
**而當優先性相同時依據相依性的運算方向執行。**

## 加減乘除優先性

以 `var a = 2 * 2 + 2 * 3;` 為例子

![加減乘除優先性](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8A%A0%E6%B8%9B%E4%B9%98%E9%99%A4%E5%84%AA%E5%85%88%E6%80%A7.jpg?alt=media&token=f9bfa0e0-02a3-45fd-96dd-98691b64506a)

因為 *(乘號)的優先性大於 +(加號)，所以會先進行乘的動作，接著乘出來的數字就是 +(加號)的運算元，這也符合描述的優先性。

<!--more-->

## 等號優先性

等號的相依性是由右至左，而且優先性其實不高。

![等號優先性](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%AD%89%E8%99%9F%E5%84%AA%E5%85%88%E6%80%A7.jpg?alt=media&token=9143852e-2b02-4be5-b1f0-bbf4c2fdebf0)

```
var a = 1;
var b = 2;
a = b = 3;
console.log(a, b); // 3 , 3
```

因為等號是由右至左，所以拆解出來會像下面這樣

```
b = 3; // 3
a = b; // 3
```

但是這邊要注意的一點是，a 雖然是 3 沒有錯，但是它是取到 b 的**值**，所以 a 取到的是 b 的回傳結果。

<br>

接下來看到另外一個範例

```
var b = {};
Object.defineProperty(b, 'a', {
    value: 2,  // 值 = 2
    writable: false // 不可寫入
});
var a = 1;
a = b.a = 1;

console.log(a, b.a) //  1 , 2
```

a 會回傳 1 的原因是因為**所有表達式都會回傳值**，如果沒有去接收它的話，它會立即釋放不會儲存，變成只是一個過程。(如下圖)
而 `=` 也是表達式，它的功能是將右側的值賦予至左側，居然它是表達式它就必須要回傳 **值**，而它回傳的值都是以右側來做表示的。

![範例](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%84%AA%E5%85%88%E6%80%A7%E7%AF%84%E4%BE%8B.jpg?alt=media&token=d1d55e77-42b9-4080-a8a1-ffa006cbdfee)

## 大於小於的優先性

![大於小於優先性](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%A4%A7%E6%96%BC%E5%B0%8F%E6%96%BC%E5%84%AA%E5%85%88%E6%80%A7.jpg?alt=media&token=ea744514-c2bb-470d-a8c6-9e58b88efb9b)

```
console.log(1 < 2 < 3); // true

// 可以拆解成
console.log(1 < 2); // true
console.log(true < 3); // true
console.log(1 < 3); //true 會因為型別的轉換會轉換成 1


console.log(3 > 2 > 1); // false

// false 的原因，會被拆解成下列這樣
console.log(3 > 2); // true
console.log(true > 1); // false
console.log(1 > 1); // false 會因為型別的轉換會轉換成 1
```