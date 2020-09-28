---
title: JavaScript核心篇：使用建構式自定義原型
date: 2020-03-13 14:30:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 使用建構式自定義原型

```
function Dog(name, color, size) {
	this['name'] = name;
	this['color'] = color;
	this['size'] = size;
};

var Bibi = new Dog('比比', '棕色', '小');
console.log(Bibi);
```

![使用建構式自定義原型-1](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E4%BD%BF%E7%94%A8%E5%BB%BA%E6%A7%8B%E5%BC%8F%E8%87%AA%E5%AE%9A%E7%BE%A9%E5%8E%9F%E5%9E%8B-1.jpg?alt=media&token=62a17874-1da6-44db-a2d4-55330f108ba7)

<!--more-->

透過 `new` 的運算子每次都會產生一個新的物件。

在上圖可以看到後面用 `new` 建構出來的 `Bibi` 原型是指向 `Dog` 的。


## 新增一個原型的方法

```
function Dog(name, color, size) {
	this['name'] = name;
	this['color'] = color;
	this['size'] = size;
};

var Bibi = new Dog('比比', '棕色', '小');
var Pupu = new Dog('噗噗', '白色', '大');

Dog.prototype.bark = function () {
	console.log(this.name + ' 吠叫');
};

console.log(Bibi.bark());  // 比比 吠叫
console.log(Pupu.bark());  // 噗噗 吠叫
```

![使用建構式自定義原型-2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E4%BD%BF%E7%94%A8%E5%BB%BA%E6%A7%8B%E5%BC%8F%E8%87%AA%E5%AE%9A%E7%BE%A9%E5%8E%9F%E5%9E%8B-2.jpg?alt=media&token=c765fd31-7e56-4276-81c5-fa55d5ae8aa9)

這邊可以看到`Dog`作為原型，能夠讓實體共用原型的屬性及方法，所以我們在`Dog`裡面新增一個方法就能夠讓下面的實體共用囉！

這樣的好處是能夠減少記憶體的消耗，因為原型的方法能夠讓下面的實體共用。