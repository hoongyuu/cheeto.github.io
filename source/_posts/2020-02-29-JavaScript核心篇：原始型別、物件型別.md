---
title: JavaScript核心篇：原始型別、物件型別
date: 2020-02-29 19:40:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 原始型別、物件型別

JavaScript 主要分為 原始型別、物件型別 兩大類。


## 原始型別

* Boolean 布林
* Null 空值
* Undefined 未定義
* Number 數值
* String 字串

**ES6**

* Bight 整體數值
* Symbol

```
var a, b, c, d;
console.log(typeof a); // undefined
a = 1;
console.log(typeof a); // number
a = '文字';
console.log(typeof a); // string
b = true;
console.log(typeof b); // boolean
c = {};
console.log(typeof c); // object
d = null; // 音標 nʌl
console.log(d , typeof d); // object
console.log(typeof e); // undefined
```

* null 會被 typeof 判定成是 object 是 JavaScript 長久以來的 bug。
* 正常來說沒有宣告 e 為變數 `console.log(e)` 的話會出現 not defined，但是 **not defined 在 typeof 裡面會把它轉換成 undefined**，這是 typeof 針對 not defined 的一個保護措施。


## 包裹物件

>[基本型別包裹器](https://ithelp.ithome.com.tw/articles/10193902)

```
var a = 'ming';
console.log(a);
var e = new String(a);
console.log(e);
```

![包裹物件](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8C%85%E8%A3%B9%E7%89%A9%E4%BB%B6.jpg?alt=media&token=fbdb84da-ad44-436c-a4ef-e5a1d4938c63)

這邊要注意的是 e 經過 new String() 的轉化已經變成一個物件了。而包裹物件的功能可以在 _proto_ 裡面看到。