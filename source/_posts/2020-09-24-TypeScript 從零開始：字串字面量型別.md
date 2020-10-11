---
title: TypeScript 從零開始：字串字面量型別
date: 2020-09-24 14:20:00
tags:
  - TypeScript
categories: 
  - TypeScript
---

# TypeScript 從零開始：字串字面量型別

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FXZBuk51.png?alt=media&token=190cc704-893e-4dea-ac8c-65043a94280d)

TypeScript 是 JavaScript 的超集合，將強型別帶入 JavaSript，並提供對 ES6 的支援，而 TypeScript 由 Microsoft 開發，程式開源於 **GitHub** 上。

> 學習資源參考 [TypeScript 新手指南](https://willh.gitbook.io/typescript-tutorial/)

<!--more-->

# 字串字面量型別 ( String Literal )

**字串字面量型別**是能夠透過 `type` 來定義，限制**值**只能是限定的哪幾個，如果設定的值不是限定的那幾個的話，會報錯。

<br>

```
// 編譯前
type animal = '小狗' | '小貓' | '小鳥';

interface pet {
  animal: animal,
  color: string,
  size: string
}

let myPet: pet = {
  animal: '小狗',
  color: '灰色',
  size: '小型'
}

// 編譯後
var myPet = {
    animal: '小狗',
    color: '灰色',
    size: '小型'
};
```

因為 `animal` 裡面本來就有 '小狗' 這個值，所以可以正常的運行。

```
type animal = '小狗' | '小貓' | '小鳥';

interface pet {
  animal: animal,
  color: string,
  size: string
}

let myPet: pet = {
  animal: '小強',
  color: '灰色',
  size: '小型'
}

// 會報錯：Type '"小強"' is not assignable to type 'animal'.
```

報錯的內容是說，小強並沒有在 `animal` 設定的特定值裡面，所以不能使用。