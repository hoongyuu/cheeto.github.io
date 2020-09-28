---
title: JavaScript核心篇：物件擴充的修改與調整
date: 2020-03-14 19:40:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 物件擴充的修改與調整

這個章節一共會教三個物件方法：

* preventExtensions - 防止擴充
* seal - 封裝
* Freeze - 凍結


## preventExtensions - 防止擴充

`preventExtensions`用意是無法新增屬性。

```
var person = {
  a: 1,
  b: 2,
  c: {}
}

Object.preventExtensions(person);
console.log('是否可被擴充', Object.isExtensible(person));
console.log('person a 的屬性特徵', Object.getOwnPropertyDescriptor(person, 'a'));

// 調整屬性
person.a = 'a';

// 新增屬性
person.d = 'd';  // 無效，因為防止擴充無法新增屬性

// 巢狀屬性調整
person.c.a = 'ca'; // 有效，因為防止擴充只能限制第一層

// 調整特徵
Object.defineProperty(person, 'a', {
  configurable: false
});

// 刪除
delete person.b;

// 結果
console.log('person 物件', person);
console.log('person a 屬性特徵(嘗試修改後)', Object.getOwnPropertyDescriptor(person, 'a'));
```

![物件擴充的修改與調整-1](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%89%A9%E4%BB%B6%E6%93%B4%E5%85%85%E7%9A%84%E4%BF%AE%E6%94%B9%E8%88%87%E8%AA%BF%E6%95%B4-1.jpg?alt=media&token=cae38dad-00dc-4327-a2df-98cd40e5411f)

我們可以看到 `preventExtensions` 主要的功能就是防止擴充，但是它的作用只能在指定物件的第一層屬性。因為物件是傳址的，所以只能對當下的屬性作動。

所以我們去刪除屬性、調整屬性都是被允許的。

## seal - 封裝

`seal` ： 讓指定物件的屬性無法新增、刪除，也無法重新配置特徵，但是可以調整屬性值。

* 預設會讓物件加上 `preventExtensions`

```
var person = {
	a: 1,
	b: 2,
	c: {}
}

Object.seal(person);
console.log('是否可被擴充', Object.isExtensible(person));
console.log('是否被 封裝 ', Object.isSealed(person));
console.log('person a 的屬性特徵', Object.getOwnPropertyDescriptor(person, 'a'));

// 調整屬性
person.a = 'a';  // 有效，seal可以調整屬性值

// 新增屬性
person.d = 'd';  // 無效，seal 無法新增、刪除屬性

// 巢狀屬性調整
person.c.a = 'ca'; // 有效，因為 seal 只能限制第一層

// 調整特徵
Object.defineProperty(person, 'a', {
	writable: false  // 無效，seal 無法重新配置特徵
});

// 刪除
delete person.b; // 無效， seal 無法新增、刪除屬性

// 結果
console.log('person 物件', person);
console.log('person a 屬性特徵(嘗試修改後)', Object.getOwnPropertyDescriptor(person, 'a'));
```

![物件擴充的修改與調整-2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%89%A9%E4%BB%B6%E6%93%B4%E5%85%85%E7%9A%84%E4%BF%AE%E6%94%B9%E8%88%87%E8%AA%BF%E6%95%B4-2.jpg?alt=media&token=59839c23-9cad-4eb3-9185-ebcb917ffe0c)

可以看到`seal`不能被新增、刪除屬性，也無法重新配置特徵，但是可以被調整屬性值。

`seal` 跟 `preventExtensions` 一樣只能限制到第一層的屬性。主要是因為物件是傳址的，所以只能對當下的屬性作動。


## freeze

* 物件會加上 `seal`，且無法調整值。

```
var person = {
  a: 1,
  b: 2,
  c: {}
}

Object.freeze(person);
console.log('是否可被擴充', Object.isExtensible(person));
console.log('是否被 封裝 ', Object.isSealed(person));
console.log('是否被 凍結 ', Object.isFrozen(person));
console.log('person a 的屬性特徵', Object.getOwnPropertyDescriptor(person, 'a'));

// 調整屬性
person.a = 'a';  // 無效， freeze 無法調整值

// 新增屬性
person.d = 'd';  // 無效，freeze 無法新增、刪除屬性

// 巢狀屬性調整
person.c.a = 'ca'; // 有效，因為 freeze 只能限制第一層

// 刪除
delete person.b; // 無效， freeze 無法新增、刪除屬性

// 結果
console.log('person 物件', person);
console.log('person a 屬性特徵(嘗試修改後)', Object.getOwnPropertyDescriptor(person, 'a'));
```

![物件擴充的修改與調整-3](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%89%A9%E4%BB%B6%E6%93%B4%E5%85%85%E7%9A%84%E4%BF%AE%E6%94%B9%E8%88%87%E8%AA%BF%E6%95%B4-3.jpg?alt=media&token=3669ec70-f01c-4bb6-b0df-04d46c9394bf)

`freeze` 有 `seal` 的所有功能，但是它又多了一個**不能調整值**的功能。

還有另外一點，它在調整屬性特徵時 `console.log` 會跳錯。