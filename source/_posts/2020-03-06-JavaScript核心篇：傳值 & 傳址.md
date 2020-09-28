---
title: JavaScript核心篇：傳值 & 傳址
date: 2020-03-06 13:47:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 傳值 & 傳址

> [本章參考](https://ithelp.ithome.com.tw/articles/10191057)

## 傳值

所有的基本型別都是「傳值」。

```
var a = 10;
var b = a;

a = 100;
console.log(a, b); // 100, 10
```

這邊可以看到 `b = a` 但是`a`的值改變了之後`b`卻維持在原位，這是因為**基本型別**的傳遞是利用複製的，所以 `b = a` 的值是複製`a`的值而已。

可以看作`a`、`b`兩個都是不同的個體。

所以之後`a`不管做了什麼樣的更新，都跟`b`不會有任何的關係。這種方式稱為「**傳值**」。

## 傳址

所有的物件型別都是「傳址」。接下來就讓我們來看看什麼是傳址吧！

```
var person = {
    name: '小明',
    money: 1000
};
var person2 = person;
person2.name = '杰倫';
```

會變成下面這樣 ↓

![傳址測試](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%82%B3%E5%9D%80%E6%B8%AC%E8%A9%A6.jpg?alt=media&token=9d153fa4-67ae-4e91-bc8b-63fb2695b450)

為什麼會有這樣的變動呢？我們用下面這個圖片來解釋：

![傳址](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%82%B3%E5%9D%80.jpg?alt=media&token=d445d522-5b54-4013-8435-9dce192efb59)

`var person2 = person` 的時候，`person` 其實是把記憶體參考位址傳給了 `person2`，因為它們都是同一個位址，所以就算 `person2` 把記憶體參考位址的東西變動了，在同一個位址的 `person` 也當然會跟著變動了。

而這種方式就稱為「**傳址**」。

<br>

接下來我們看下一個範例

```
var person = {
    name: '小明'
};
var person2 = person;
person2 = {
    name: '小明'
}
console.log(person == person2); // false
```

讓我們用下圖解釋為什麼會這樣

![傳址2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%82%B3%E5%9D%802.jpg?alt=media&token=4dc7d4d6-4b0e-46fd-90b5-0ae0cf8c40c5)

這邊可以看到如果 `person2` 指向一個新的物件的話，它其實會傳入一個新的位址上。

這時候 `person` 跟 `person2` 就不會有任何關聯了。