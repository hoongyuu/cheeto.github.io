---
title: JavaScript核心篇：原型在哪裡？
date: 2020-03-12 18:47:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 原型在哪裡？

> JavaScript 是一門物件導向的程式語言，因為沒有 Class，所以它的繼承方法是透過 「原型」(prototype) 來進行實作。

原形的特性
* 一樣具有物件的特性
* 向上查找
* 原型可共用方法及屬性

當我們嘗試在某個物件找一個它本身並不存在的屬性時，它會往上(原型物件)找尋，直到找到最頂層級時，都會找到`Object.prototype`才會停止。


## JS當中原型跟實體都是物件，而兩者都有屬性及方法

![原形鍊-概念](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8E%9F%E5%BD%A2%E9%8D%8A-%E6%A6%82%E5%BF%B5.jpg?alt=media&token=4a3ff0d0-1342-4c44-8429-e37af5a739bd)

這邊可以看到實體可以繼承原型的屬性及方法，實體也能夠自定義自己的屬性及方法。

![原形鍊-圖解](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8E%9F%E5%BD%A2%E9%8D%8A-%E5%9C%96%E8%A7%A3.jpg?alt=media&token=4869693b-8321-4314-9aed-ea84607e5bab)

這邊可以看到原型找不到屬性或方法時會往它的原型去尋找，假設它沒有找到的話，它會繼續往上面的原型去找，直到找到最頂層級。

原型的方法都能夠用**點運算子呼叫出來**。


![原形鍊-圖解2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8E%9F%E5%BD%A2%E9%8D%8A-%E5%9C%96%E8%A7%A32.jpg?alt=media&token=aa20acda-dbc0-41a7-b822-dfbaa0139dcd)

如果一個原型新增了兩個實體的話，那這兩個實體都會繼承原型的屬性。


```
var a = [1, 2, 3];
console.log(a, a[1], a.length);
    
a.forEach( (i) => {console.log(i)} )
```

![原形鍊-原型說明](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8E%9F%E5%BD%A2%E9%8D%8A-%E5%8E%9F%E5%9E%8B%E8%AA%AA%E6%98%8E.jpg?alt=media&token=e5fe60e0-9033-4028-a56d-1873edfb90eb)

這邊可以看到 `a` 的原型是 `array`。

而只要是**實體都能夠繼承原型的屬性及方法**，這邊也能夠看到 `a` 能夠使用 `array` 的 `forEach()` 這個方法。

<br>

這邊我們用 `__proto__` 來新增原型的方法。

> 這個原型的方法非正規，這邊只是示範用

```
var a = [1, 2, 3];

a.__proto__.getLast = function (e) {
    //傳入該陣列最後一個值
    return this[this.length -1];
}

var b = [4, 5, 6];

//原型共用特性
console.log(a.getLast());  // 3
console.log(b.getLast());  // 6
```

這邊如果輸入 `a` 跟 `b` 可以發現這點


![原形鍊-原型說明2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8E%9F%E5%BD%A2%E9%8D%8A-%E5%8E%9F%E5%9E%8B%E8%AA%AA%E6%98%8E2.jpg?alt=media&token=31134655-5845-4700-a889-a485dc31dfe8)

![原形鍊-原型說明3](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8E%9F%E5%BD%A2%E9%8D%8A-%E5%8E%9F%E5%9E%8B%E8%AA%AA%E6%98%8E3.jpg?alt=media&token=662ad252-35c3-4bfd-b2ec-5d347016d433)

它們同樣都繼承了 `array` 的 `getLast()` 這個方法，所以都能夠共用 `getLast()` 這個方法。