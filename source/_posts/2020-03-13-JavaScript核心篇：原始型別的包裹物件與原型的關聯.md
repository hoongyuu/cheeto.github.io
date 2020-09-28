---
title: JavaScript核心篇：原始型別的包裹物件與原型的關聯
date: 2020-03-13 18:20:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 原始型別的包裹物件與原型的關聯

```
var a = 'a';
console.log(a.toUpperCase()); // A
```

這邊可以看到我們利用 `toUpperCase()` 的方法來讓本來`a`變成大寫，而`toUpperCase()`其實就是原型的方法。

```
var b = new String('bcde');
console.log(b);
```

![原始型別的包裹物件與原型的關聯-1](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8E%9F%E5%A7%8B%E5%9E%8B%E5%88%A5%E7%9A%84%E5%8C%85%E8%A3%B9%E7%89%A9%E4%BB%B6%E8%88%87%E5%8E%9F%E5%9E%8B%E7%9A%84%E9%97%9C%E8%81%AF-1.jpg?alt=media&token=b3e6c7bc-c6c5-4fec-8440-34f59cdc384f)

雖然利用了包裹物件會讓純值變成物件型別，但是我們可以利用這個方法來看原型裡面的所有屬性及方法。

<!--more-->

```
var b = new String('bcde');

String.prototype.lastText = function (e) {
  return this[this.length -1];
};

console.log(b.lastText()); // e
```

可以看到我們在原型上面新增一個方法，下面的實體都能夠共用。

<br>

接下來我們試試看 `Number`

```
Number.prototype.secondPower = function (e) {
  return this * this ;
};

var num = 5;
console.log(num.secondPower());  // 25
```

這邊也能夠看到原型能夠共用。

<br>

再來看下一個範例
```
Date.prototype.getFullDate = function (e) {
	var dd = String(this.getDate());
	var mm = String(this.getMonth() +1);
	var yyyy = String(this.getFullYear());
  
	var today = yyyy + '/' + mm + '/' + dd;
	return today
}

var date = new Date();
console.log(date.getFullDate()); // 2020/3/12 ((符合現在日期
```

這個章節的重點就是純值其實也能使用**它的原型**的屬性及方法。