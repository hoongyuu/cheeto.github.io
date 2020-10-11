---
title: TypeScript 從零開始：任意值、預設型別判定
date: 2020-09-12 16:00:00
tags:
  - TypeScript
categories: 
  - TypeScript
---

# TypeScript 從零開始：任意值、預設型別判定

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FXZBuk51.png?alt=media&token=190cc704-893e-4dea-ac8c-65043a94280d)

TypeScript 是 JavaScript 的超集合，將強型別帶入 JavaSript，並提供對 ES6 的支援，而 TypeScript 由 Microsoft 開發，程式開源於 **GitHub** 上。

> 學習資源參考 [TypeScript 新手指南](https://willh.gitbook.io/typescript-tutorial/)

<!--more-->

# TypeScript：任意值

除了前一個上一篇文章講到的基本型別宣告外，TS 也有可以像 JS 一樣能夠任意變換型別的**任意值型別**。

## 任意值型別

```
// 編譯前
let anyTS: any = 'Cheeto';
anyTS = 123;
anyTS = true;

// 編譯後
var anyTS = 'Cheeto';
anyTS = 123;
anyTS = true;
```

只要使用 any( 任意值型別 )，就跟 JS 一樣可以任意變換型別。

## 未宣告型別的變數

如果再 TS 當中沒有宣告型別的話，那預設就會是 any( 任意值型別 )。

```
// 編譯前
let anyTS;
anyTS = 55987;
anyTS = 'Cheeto';

// 編譯後
var anyTS;
anyTS = 55987;
anyTS = 'Cheeto';
```

如果宣告變數沒有賦予值的話，TS 就會預設判定為 any( 任意值型別 )。

```
let anyTS;
anyTS = 55987;
anyTS = 'Cheeto';

// 上方 ↑ === 下方 ↓

let anyTS: any;
anyTS = 55987;
anyTS = 'Cheeto';
```

# 預設型別判定

當你在 TS 撰寫時，沒有賦予變數任何一個型別判定的話，它會從你賦予的值裡面去判別。

```
let myName = 'Cheeto';
myName = 9487;

// 會報錯： Type 'number' is not assignable to type 'string'.
```

以上方範例解釋，因為 `myName` 的變數是 `String`，所以在 TS 當中它的判定型別就會是 `String`。

```
let myName = 'Cheeto';
let num = 9487;

// 上方 ↑ === 下方 ↓

let myName: string = 'Cheeto';
let num: number = 9487;
```