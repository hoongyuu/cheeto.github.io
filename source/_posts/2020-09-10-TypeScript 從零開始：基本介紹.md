---
title: TypeScript 從零開始：原始型別
date: 2020-09-10 14:05:00
tags:
  - TypeScript
categories: 
  - TypeScript
---

# TypeScript 從零開始：原始型別

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FXZBuk51.png?alt=media&token=190cc704-893e-4dea-ac8c-65043a94280d)

TypeScript 是 JavaScript 的超集合，將強型別帶入 JavaSript，並提供對 ES6 的支援，而 TypeScript 由 Microsoft 開發，程式開源於 **GitHub** 上。

> 學習資源參考 [TypeScript 新手指南](https://willh.gitbook.io/typescript-tutorial/)

<!--more-->

## 什麼是超集合 ( SuperSet ) ？

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FTypeScript%E8%B6%85%E9%9B%86%E5%90%88.png?alt=media&token=bcc041af-47e3-415d-9569-d17061bf5b72)
> 示意圖 ↑

JavaScript 是一個語言的集合，但是 TypeScript 除了有完整 JavaScript 之外，自己又額外增加了各種功能，所以是 JavaScript 的超集合。

在 TS 的檔案當中是支援 ES6 的語法的，所以就算使用 ES6 也是沒有問題的，不過必須透過 TS 的編譯器才能編譯為 JS 檔，瀏覽器才能進行解讀。

# 原始資料型別

在 TypeScript 當中宣告變數時，可以透過 `:` 來檢查型別，那就讓我們繼續下去吧！

## 布林值 ( boolean )

正常的編譯的情況下會是這樣 ↓

```
// 編譯前
let booleanTS: boolean = true;

// 編譯後
var booleanTS = true;
```

那如果變數不是布林值呢？

```
// 編譯前
let booleanTS: boolean = { name: 'Cheeto' };

// 編譯時會跳錯： Type { name: 'Cheeto' } is not assignable to type 'boolean'.
// 但是就算是報錯了，還是會編譯出 JS 的檔案唷！

// 編譯後
var booleanTS = { name: 'Cheeto' };
```

這邊就能看出 TypeScript 的其中一個特性，它是會通知你哪裡出現狀況，但是並不會強制修改。

## 數值 ( Number )

```
// 編譯前
let basicNum: number = 123;
let nanNum: number = NaN;
let infinityNum: number = Infinity;

// 編譯後
var basicNum = 123;
var nanNum = NaN;
var infinityNum = Infinity;
```

在 `Number` 當中只要是 JS 的基本型別當中是屬於 `Number` 的就不會出現錯誤的資訊，都是能夠正常編譯。

## 字串 ( String )

```
// 編譯前
let myName: string = 'Cheeto';
let myBro: string = 'Nian'
let str: string = `My name is ${ myName }, and my bro name is ${ myBro }.`

// 編譯後
var myName = 'Cheeto';
var myBro = 'Nian';
var str = "My name is " + myName + ", and my bro name is " + myBro + ".";
```

這邊可以看到我在編譯前使用的是 ES6 的**樣板字面值**，但是在編譯過程中它會轉換成透過 `+` 的方式組成的字串。

## 空值 ( Void )

在 TS 當中，可以使用 `Void` 來宣告沒有回傳值的函式來進行查驗。

```
// 編譯前
const newFunc = (): void => {
  const myName = 'Cheeto';
  const myBro = 'Nian';
}

function func1 (): void {
  const myName = 'Cheeto';
  const myBro = 'Nian';
}

// 編譯後
var newFunc = function () {
    var myName = 'Cheeto';
    var myBro = 'Nian';
}
function func1() {
    var myName = 'Cheeto';
    var myBro = 'Nian';
}
```

## `Null` & `Undefined`

在 TS 當中，也能利用 `Null` & `Undefined` 來進行型別辨認：

```
// 編譯前
let undefinedTS: undefined = undefined;
let nullTS: null = null;

// 編譯後
var undefinedTS = undefined;
var nullTS = null;
```