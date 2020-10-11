---
title: TypeScript 從零開始：聯合型別
date: 2020-09-14 18:23:00
tags:
  - TypeScript
categories: 
  - TypeScript
---

# TypeScript 從零開始：聯合型別

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FXZBuk51.png?alt=media&token=190cc704-893e-4dea-ac8c-65043a94280d)

TypeScript 是 JavaScript 的超集合，將強型別帶入 JavaSript，並提供對 ES6 的支援，而 TypeScript 由 Microsoft 開發，程式開源於 **GitHub** 上。

> 學習資源參考 [TypeScript 新手指南](https://willh.gitbook.io/typescript-tutorial/)

<!--more-->

# 聯合型別

在 TS 當中也是可以賦予多個型別，這樣也有容錯的空間。

```
// 編譯前
let myName: string | number | boolean = 'Cheeto';
myName = 9487;
myName = false;

// 編譯後
var myName = 'Cheeto';
myName = 9487;
myName = false;
```

在每一個型別之間透過 `|` 來間隔，那就可以做到多個型別的判定。

## 利用到 `function`

TS 把你想得到的都想到了，當然也能夠在 `function` 的參數當中進行判別啦。

```
// 編譯前
function wallet(money: number | string) {
  console.log(money)
}
wallet(9487); // 9487 
wallet('Cheeto');  // Cheeto

// 編譯後
function wallet(money) {
    console.log(money);
}
wallet(9487); // 9487
wallet('Cheeto'); // Cheeto
```

像上方這樣就能夠在**參數**當中進行聯合型別判定。