---
title: JavaScript核心篇：原型鍊、建構函式整體結構概念
date: 2020-03-13 23:20:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 原型鍊、建構函式整體結構概念

原型鍊是實體可以繼承原型，而原型又可以繼承在它之上的原型，直到最頂層級(null)為止，而`null`也是原型鍊的最後一個鏈結。

就像下面這張圖 ↓

![原型鍊、建構函式整體結構概念-1](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8E%9F%E5%9E%8B%E9%8D%8A%E3%80%81%E5%BB%BA%E6%A7%8B%E5%87%BD%E5%BC%8F%E6%95%B4%E9%AB%94%E7%B5%90%E6%A7%8B%E6%A6%82%E5%BF%B5-1.jpg?alt=media&token=33666420-9e14-4595-89c4-90e96d6f1382)

<!--more-->

<br>


* 建構函式會連接到 `constructor` 
* `__proto__` 可以向上尋找原型

![原型鍊、建構函式整體結構概念-2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8E%9F%E5%9E%8B%E9%8D%8A%E3%80%81%E5%BB%BA%E6%A7%8B%E5%87%BD%E5%BC%8F%E6%95%B4%E9%AB%94%E7%B5%90%E6%A7%8B%E6%A6%82%E5%BF%B5-2.jpg?alt=media&token=56b911ca-a91c-49af-9987-8925ff93a59f)

我們可以使用程式碼來驗證看看

```
function Animal(family) {
	this['kingdom'] = '動物界';
	this['family'] = this.family || '人科';
};

Animal.prototype.move = function name(params) {
	console.log(this['name'] + ' 移動');
};

function Dog(name, color, size) {
	// 利用 call 指定 this 能夠指向每一個實體
	Animal.call(this, '犬科');
	this['name'] = name;
	this['color'] = color || '黑色';
	this['size'] = size || '小';
}

Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = 'Dog';
Dog.prototype.bark = function (e) {
	console.log(this['name'] + ' 吠叫');
};


var Bibi = new Dog('比比', '棕色', '小');

// 驗證原型鍊結構
console.log(Bibi['__proto__'] === Dog['prototype']); //true
console.log(Bibi['__proto__']['__proto__'] === Animal['prototype']);  //true
console.log(Bibi['__proto__']['__proto__']['constructor'] === Animal); //true
console.log(Bibi['__proto__']['__proto__']['__proto__']['__proto__'] === null); //true
```

上方程式碼就能夠驗證上面那張圖所描述的，`__proto__` 可以向上尋找原型，而 `__proto__` 跟上面第一層原型的 `prototype` 是完全相等的。

<br>

接下來我們可以驗證看看函式的繼承

```
console.log(Bibi['__proto__'] === Function['prototype']); // flase
console.log(Dog['__proto__'] === Function['prototype']); // true
console.log(Animal['__proto__'] === Function['prototype']); // true
console.log(Object['__proto__'] === Function['prototype']); // true
```

這邊可以看到只要是函式，都會繼承函式的原型。