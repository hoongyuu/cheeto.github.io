---
title: TypeScript 從零開始：介面 ( interface )
date: 2020-09-16 17:40:00
tags:
  - TypeScript
categories: 
  - TypeScript
---

# TypeScript 從零開始：介面 ( interface )

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FXZBuk51.png?alt=media&token=190cc704-893e-4dea-ac8c-65043a94280d)

TypeScript 是 JavaScript 的超集合，將強型別帶入 JavaSript，並提供對 ES6 的支援，而 TypeScript 由 Microsoft 開發，程式開源於 **GitHub** 上。

> 學習資源參考 [TypeScript 新手指南](https://willh.gitbook.io/typescript-tutorial/)

<!--more-->

# 介面 ( interface )

在 `interface` 當中可以宣告它有哪些屬性，也能為該屬性宣告型別，但是 `interface` 只是一個輪廓，還是要再去把它的細節補上才能使用。

下面就讓我們繼續學習吧 ↓

```
// 編譯前
interface Person {
  name: string;
  age: number;
}

let fufu: Person = {
  name: '小富',
  age: 25,
}

// 編譯後
var fufu = {
    name: '小富',
    age: 25
};
```

當我們在宣告 `interface` 的時候，**命名的首字通常會使用大寫**，比較好避免跟一般的 `class` 搞混。

在介面當中不能少任何一個屬性：

```
interface Person {
  name: string;
  age: number;
}

let fufu: Person = {
  name: '小富',
}

// 會報錯： Property 'age' is missing in type '{ name: string; }' but required in type 'Person'.
```

在介面當中不能多任何一個屬性：

```
interface Person {
  name: string;
  age: number;
}

let fufu: Person = {
  name: '小富',
  age: 25,
  hair: '黑色',
}

// 會報錯： Type '{ name: string; age: number; hair: string; }' is not assignable to type 'Person'.
```

由此可知，在使用 `interface` 宣告的時候，必須它所設定的輪廓一模一樣，不能多也不能少！

## 可選屬性

在 `interface` 當中我不會每次都想要一模一樣呀，那我們該怎麼辦呢？

這時候就可以來學點**可用屬性**啦！

```
// 編譯前
interface Person {
  name: string;
  age?: number;
}

let fufu: Person = {
  name: '小富',
}

// 編譯後
var fufu = {
    name: '小富'
};
```

只要在屬性後面加上 `?`，那它就可以變成可有可無的屬性了！

## 任意屬性

前面講到可選屬性能夠讓屬性可有可無，但是我們想要多新增一個屬性該怎麼辦呢？

就讓我們繼續學下去吧！

```
// 編譯前
interface Person {
  name: string;
  age?: number;
  [propName: string]: any;
}

let fufu: Person = {
  name: '小富',
  age: 25,
  hair: 9487,
}

// 編譯後
var fufu = {
    name: '小富',
    age: 25,
    hair: 9487
};
```

任意屬性可以使用 `[propName: string]` 來定義。

但是如果我們把任意值換成型別判定的話，那麼**確定屬性和可選屬性的型別都必須是它的型別的子集**：

```
interface Person {
  name: string;
  age?: number;
  [propName: string]: string;
}

let fufu: Person = {
  name: '小富',
  age: 25,
  hair: '黑色',
}

這邊就會報錯，只要在任意屬性上定義型別，那所有的確定屬性跟可選屬性的型別都必須是它的型別子集。
```

**只要在任意屬性上定義型別，那所有的確定屬性跟可選屬性的型別都必須是它的型別子集。**

任意屬性的這個特點要特別注意。