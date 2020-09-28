---
title: JavaScript核心篇：屬性特徵是什麼？
date: 2020-03-14 15:40:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 屬性特徵是什麼？

```
// Object.defineProperty
// 屬性，調整屬性特徵
// 1. 值、 2. 可否寫入、 3. 可否被刪除、 (物件, '屬性', '參數');
4. 可否被列舉
// Object.defineProperty
var person = {
    a: 1,
    b: 2,
    c: 3
};

console.log(person);  // {a: 1, b: 2, c: 3}

Object.defineProperty(person, 'a', {
    // 1. 值
    value: 4,
    // 2. 可否寫入
    writable: true, //預設為 true
    // 3. 可否被刪除
    configurable: true, //預設為 true
    // 4. 可否被列舉
    enumerable: true //預設為 true
});

console.log(person);  // {a: 4, b: 2, c: 3}
```

這邊可以看到 `person['a']` 的值已經被改寫了。

<!--more-->

如果我們把 `writable` 改成 false 呢？
```
var person = {
    a: 1,
    b: 2,
    c: 3
};

console.log(person);  // {a: 1, b: 2, c: 3}

Object.defineProperty(person, 'a', {
    // 1. 值
    value: 4,
    // 2. 可否寫入
    writable: false, //預設為 true
    // 3. 可否被刪除
    configurable: true, //預設為 true
    // 4. 可否被列舉
    enumerable: true //預設為 true
});

person['a'] = 10;

console.log(person);  // {a: 4, b: 2, c: 3}
```

這邊可以發現如果我們把 `writable` 改成 `false` 就能夠讓屬性不能夠被寫入。

再來我們測試 `configurable` 吧 ↓

```
var person = {
    a: 1,
    b: 2,
    c: 3
};

console.log(person);  // {a: 1, b: 2, c: 3}

Object.defineProperty(person, 'b', {
    // 可否被刪除
    configurable: false, //預設為 true
});

delete person['a'];
delete person['b'];

console.log(person);  // {b: 2, c: 3}
```

這邊可以發現我們把 `configurable` 改成 `false` 之後就能夠讓屬性無法被刪除了。

那**可否被列舉**是什麼意思呢？
```
var person = {
	a: 1,
	b: 2,
	c: 3
};

Object.defineProperty(person, "c", {
	enumerable: false
});

for (var key in person) {
	console.log("列舉", key);
};
```

![屬性特徵是什麼-1](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%B1%AC%E6%80%A7%E7%89%B9%E5%BE%B5%E6%98%AF%E4%BB%80%E9%BA%BC-1.jpg?alt=media&token=f2741b9f-4cf6-4995-8537-de2f62b4e540)

這邊可以看到我把 `c` 設定為 `enumerable: false` 之後它就無法被列舉了！

<br>

```
var person = {
	a: 1,
	b: 2,
	c: 3
};

// 淺層保護
Object.defineProperty(person, 'd', {
	value: {},
	writable: false
});

console.log(person);
person['d']['name'] = 'cheeto';
```

![屬性特徵是什麼-2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%B1%AC%E6%80%A7%E7%89%B9%E5%BE%B5%E6%98%AF%E4%BB%80%E9%BA%BC-2.jpg?alt=media&token=e1ff53dc-1416-4dc2-9181-7a5c2cb54867)

這邊如果輸入 `person['d'] = 6` 的話的確它是沒有辦法被寫入的，但是因為**物件是傳址的特性**，所以它裡面的屬性是可以被新增和修改的。

所以 `Object.defineProperty` 只能做到淺層保護的作用。切記切記

### Object.defineProperties

這個語法可以大量定義我們要定義的屬性特徵，我們來看看吧 ↓

```
var person = {
    a: 1,
    b: 2,
    c: 3
};

console.log(person); // {a: 1, b: 2, c: 3}

Object.defineProperties(person, {
    a: {
        value: 5,
        writable: false
    },
    b: {
        value: 6,
        writable: false
    },
    c: {
        value: 10,
        writable: false
    }
});

person['a'] = 15; // 因為 writable: false 所以不能被寫入
person['b'] = 20; // 因為 writable: false 所以不能被寫入
person['c'] = 30; // 因為 writable: false 所以不能被寫入

console.log(person);  // {a: 5, b: 6, c: 10}
```

這個語法跟 `Object.defineProperty` 其實差不多，但是它可以一次輸入大量的屬性去定義。