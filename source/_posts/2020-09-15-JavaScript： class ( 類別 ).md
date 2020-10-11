---
title: JavaScript： class ( 類別 )
date: 2020-09-15 21:15:00
tags:
  - JavaScript
categories: 
  - JavaScript
---

# JavaScript： class ( 類別 )

![LOGO](https://i.imgur.com/xITKDpQ.png)

首先必須知道 `class` 只是 ES6 的語法糖 ( syntactical sugar )，並不是真的以類別為基礎的物件導向，在 JavaScript 當中仍舊是原型為基礎的物件導向。

## 簡單範例

類別用 `class` 來定義，使用 `constructor` 來定義建構函式。

```
class Animal {
  constructor (family, name, color, size) {
    this.family = family;
    this.name = name;
    this.color = color;
    this.size = size;
  }
  move () {
    console.log(`${this.name} 移動`);
  }
}

const fufu = new Animal('小狗', '富富', '黑色', '小型');
fufu.move(); // 富富 移動
```

> 類別命名時建議使用大駝峰命名法

<!--more-->

## 類別繼承

類別可以通過 `extends` 語法來繼承，子類別可以透過 `super` 來呼叫父類別的建構函式和方法。

```
class Animal {
  constructor (family) {
    this.family = family;
  }
  move () {
    console.log(`${this.name} 移動`);
  }
}

class Dog extends Animal {
  constructor (family, name, color, size) {
    super(family); // 呼叫父類別的 constructor(name)
    this.name = name;
    this.color = color;
    this.size = size;
  }
  bark () {
    console.log(`${this.name} 吠叫汪汪`);
  }
}

const fufu = new Dog('小狗', '富富', '黑色', '小型');
// ↓ 回傳： 小狗 富富 黑色 小型
console.log(fufu.family, fufu.name, fufu.color, fufu.size);
fufu.move(); // 富富 移動
fufu.bark(); // 富富 吠叫汪汪
```

透過繼承的方式 `Dog` 也繼承到了 `animal` 的方法。

## getter 與 setter

在類別定義中可以使用 `get` & `set` 作為類別方法的修飾符，使用 `get` & `set` 可以改變屬性的賦值和讀取效果。

```
class Person {
  constructor (name, hairColor) {
    this.name = name;
    this.hair = hairColor;
  }
  set hair (val) {
    console.log(`${ this.name } 的頭髮是${ val }的`);
  }
  get hair () {
    return '黑色';
  }
}

const fufu = new Person('富富', '金色'); // 富富 的頭髮是金色的
console.log(fufu.hair); // 黑色
fufu.hair = '紅色'; // 富富 的頭髮是紅色的
```

如果我們把 `fufu` 呼叫出來，可以發現 `hair` 是顯示 (...) 的狀態，點開來之後會是黑色的，這主要是跟 getter 有關。

## 靜態方法 ( static )

使用 `static` 修飾符就稱為靜態方法，靜態方法不需要實體化，它是透過類別直接呼叫的。

```
class Person {
  constructor (name) {
    this.name = name;
  }
  static sayHi () {
    console.log('Hello World!');
  }
}

const fufu = new Person('小富');
Person.sayHi(); // Hello World!
fufu.sayHi(); // 報錯：fufu.sayHi is not a function
```

在靜態方法中，不能透過實例呼叫方法，只允許透過類別直接呼叫方法。

### 靜態屬性

在 ES7 之後可以使用 `static` 定義一個靜態屬性。

```
class Person {
  static name = '靜態屬性';
}

const fufu = new Person();
console.log(fufu.name); // undefined
console.log(Person.name); // 靜態屬性
```

## 實例屬性

在 ES7 當中可以直接在類別裡面定義屬性。

```
class Person {
  name = '富富'
}

const fufu = new Person();
console.log(fufu.name); // 富富
```