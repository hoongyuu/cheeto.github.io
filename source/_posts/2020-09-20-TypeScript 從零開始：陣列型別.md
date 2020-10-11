---
title: TypeScript 從零開始：陣列型別
date: 2020-09-20 21:20:00
tags:
  - TypeScript
categories: 
  - TypeScript
---

# TypeScript 從零開始：陣列型別

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FXZBuk51.png?alt=media&token=190cc704-893e-4dea-ac8c-65043a94280d)

TypeScript 是 JavaScript 的超集合，將強型別帶入 JavaSript，並提供對 ES6 的支援，而 TypeScript 由 Microsoft 開發，程式開源於 **GitHub** 上。

> 學習資源參考 [TypeScript 新手指南](https://willh.gitbook.io/typescript-tutorial/)

<!--more-->

# 陣列型別

前面介紹了基本型別，現在繼續介紹**陣列型別**吧。

```
// 編譯前
let ary: number[] = [1, 2, 3, 4, 5]
let ary: Array<number> = [1, 2, 3, 4, 5]

// 編譯後
var ary = [1, 2, 3, 4, 5];
var ary2 = [1, 2, 3, 4, 5];
```

陣列可以透過兩種方式去進行定義，不過如果定義為 `number` 的話裡面就不能出現 `number` 之外的囉！

```
let ary: number[] = [1, '2', 3, 4, 5]

// 會跳錯：Type 'string' is not assignable to type 'number'.
```

如果想要在 `ary` 上 `push()` 其他東西上去，那也必須要是 `number` 唷！

```
let ary: number[] = [1, 2, 3, 4, 5]
ary.push('6');

// 會跳錯：Argument of type 'string' is not assignable to parameter of type 'number'.
```

## 陣列型別 ( 任意值 )

比較常見的作法應該還是會用**任意值**，任意值就跟本來 JS 一樣陣列裡面可以有不同的型別。

```
// 編譯前
let ary: Array<any> = [1, '2', { num: 3 }, true, null];

// 編譯後
var ary = [1, '2', { num: 3 }, true, null];
```