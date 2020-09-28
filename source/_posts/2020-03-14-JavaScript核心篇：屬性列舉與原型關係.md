---
title: JavaScript核心篇：屬性列舉與原型關係
date: 2020-03-14 22:25:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 屬性列舉與原型關係

```
function Person(e) {};
Person['prototype']['name'] = '人類';

var casper = new Person();
casper['a'] = undefined;

console.log(casper);

console.log(casper.hasOwnProperty('a'));
console.log(casper.hasOwnProperty('b'));
console.log(casper.hasOwnProperty('name'));
```

![屬性列舉與原型關係-1](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%B1%AC%E6%80%A7%E5%88%97%E8%88%89%E8%88%87%E5%8E%9F%E5%9E%8B%E9%97%9C%E4%BF%82-1.jpg?alt=media&token=896c07dc-3a2d-4c87-a7c0-9433651a6564)

就算我們把屬性的值設定為`undefined`，屬性依舊是存在的，只是它的值是`undefined`。

`hasOwnProperty` 是對當前的物件去找屬性，不會去找原型的屬性，所以`hasOwnProperty('name')`這裡會顯示`false`。

<!--more-->

```
function Person(e) {};
Person['prototype']['name'] = '人類';

var casper = new Person();
casper['a'] = undefined;

console.log(casper);
 
for (var key in casper) {
  console.log(key);
};
```

![屬性列舉與原型關係-2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%B1%AC%E6%80%A7%E5%88%97%E8%88%89%E8%88%87%E5%8E%9F%E5%9E%8B%E9%97%9C%E4%BF%82-2.jpg?alt=media&token=c206fe28-bb46-43aa-84e8-04f50fcdef3d)

當原型的內容是可被列舉的情況下，利用`for in`一樣是可以把原型的內容列舉出來的
(**原生的屬性基本上都是不可列舉的** `enumerable: false`)


<br>

如果不想要把原型的屬性列舉出來的話可以這樣 ↓

```
for (var key in casper) {
    if (casper.hasOwnProperty(key)) {
        console.log(key);
    }
}
```

這樣就能夠只叫出`casper`的屬性，且**不會把原型可列舉的屬性叫出來**。