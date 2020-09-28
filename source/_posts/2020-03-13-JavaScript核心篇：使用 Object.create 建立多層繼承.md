---
title: JavaScript核心篇：使用 Object.create 建立多層繼承
date: 2020-03-13 21:40:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 使用 Object.create 建立多層繼承

這邊我們先看到基本的層級 ↓

```
var a = [];
// Object > Array > a(實體)

function Dog(name, color, size) {
	this['name'] = name;
	this['color'] = color;
	this['size'] = size;
};

var Bibi = new Dog('比比', '棕色', '小');
console.log(Bibi);
// Object > Dog > Bibi(實體)
```

如果我們想要在`Dog`前面新增一個層級`Object > Animal > Dog`要怎麼做呢？

<!--more-->

## Object.create() 如何運用？

```
var Bibi = {
    name: '比比',
    color: '棕色',
    size: '小',
    bark: function(){
        console.log(this.name + ' 吠叫');
    }
};

var pupu = Object.create(Bibi);
pupu.name = '噗噗';
console.log(pupu);
console.log(pupu.bark());
```
會出現 ↓

![使用 Object.create 建立多層繼承](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E4%BD%BF%E7%94%A8%20Object.create%20%E5%BB%BA%E7%AB%8B%E5%A4%9A%E5%B1%A4%E7%B9%BC%E6%89%BF.jpg?alt=media&token=aba659ce-72f1-4a41-81cf-799ea34699a4)

這邊可以發現 `pupu` 完全繼承了 `Bibi` 的所有屬性及方法。

### 我們在創造多層的原型鍊時，就會使用到 `Object.create` 的這個方法。


```
function Animal(family) {
	this.kingdom = '動物界';
	this.family = family || '人科';
};

Animal.prototype.move = function (e) {
    console.log(this.name + ' 移動');
};

function Dog(name, color, size) {
	this['name'] = name;
	this['color'] = color;
	this['size'] = size;
};

// 使用 Object.create() 讓 Dog 繼承在 Animal 身上
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.bark = function (e) {
    console.log(this.name + ' 吠叫');
}

var Bibi = new Dog('比比', '棕色', '小');
console.log(Bibi);
Bibi.bark();
Bibi.move();
```

![使用 Object.create 建立多層繼承-1](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E4%BD%BF%E7%94%A8%20Object.create%20%E5%BB%BA%E7%AB%8B%E5%A4%9A%E5%B1%A4%E7%B9%BC%E6%89%BF-1.jpg?alt=media&token=a898312d-b2d5-4dd5-9012-24da5fb208f7)

這邊還缺少了分類的部分，如果查詢 `Bibi` 的 `family` 會發現是 `undefined`，所以現在我們來新增一下科別！

```
function Animal(family) {
	this.kingdom = '動物界';
	this.family = family || '人科';
};

Animal.prototype.move = function (e) {
    console.log(this.name + ' 移動');
};

function Dog(name, color, size) {
    // 利用 call 指定 this 能夠指向每一個實體
    Animal.call(this, '犬科');
	this['name'] = name;
	this['color'] = color;
	this['size'] = size;
};

// 使用 Object.create() 讓 Dog 繼承在 Animal 身上
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.bark = function (e) {
    console.log(this.name + ' 吠叫');
}

var Bibi = new Dog('比比', '棕色', '小');
console.log(Bibi);
Bibi.bark();
Bibi.move();
```

![使用 Object.create 建立多層繼承-2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E4%BD%BF%E7%94%A8%20Object.create%20%E5%BB%BA%E7%AB%8B%E5%A4%9A%E5%B1%A4%E7%B9%BC%E6%89%BF-2.jpg?alt=media&token=6f15bd04-c7cd-46ba-b990-86b408054839)


這樣的原型鍊繼承其實還是沒有很完整喔！我們會發現`Dog`少了`constructor`

```
function Animal(family) {
	this.kingdom = '動物界';
	this.family = family || '人科';
};

Animal.prototype.move = function (e) {
    console.log(this.name + ' 移動');
};

function Dog(name, color, size) {
    // 利用 call 指定 this 能夠指向每一個實體
    Animal.call(this, '犬科');
	this['name'] = name;
	this['color'] = color;
	this['size'] = size;
};

// 使用 Object.create() 讓 Dog 繼承在 Animal 身上
Dog.prototype = Object.create(Animal.prototype);
// 這裡使用 prototype 把 constructor 補上就沒問題囉
Dog.prototype.constructor = Dog;
Dog.prototype.bark = function (e) {
    console.log(this.name + ' 吠叫');
}

var Bibi = new Dog('比比', '棕色', '小');
console.log(Bibi);
Bibi.bark();
Bibi.move();
```

![使用 Object.create 建立多層繼承-3](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E4%BD%BF%E7%94%A8%20Object.create%20%E5%BB%BA%E7%AB%8B%E5%A4%9A%E5%B1%A4%E7%B9%BC%E6%89%BF-3.jpg?alt=media&token=aaa248d0-4c75-431a-a55d-5d78d94e5b99)