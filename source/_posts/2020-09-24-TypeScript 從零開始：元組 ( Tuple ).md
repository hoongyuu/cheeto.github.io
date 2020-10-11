---
title: TypeScript 從零開始：元組 ( Tuple )
date: 2020-09-24 18:20:00
tags:
  - TypeScript
categories: 
  - TypeScript
---

# TypeScript 從零開始：元組 ( Tuple )

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FXZBuk51.png?alt=media&token=190cc704-893e-4dea-ac8c-65043a94280d)

TypeScript 是 JavaScript 的超集合，將強型別帶入 JavaSript，並提供對 ES6 的支援，而 TypeScript 由 Microsoft 開發，程式開源於 **GitHub** 上。

> 學習資源參考 [TypeScript 新手指南](https://willh.gitbook.io/typescript-tutorial/)

<!--more-->

# 元組 ( Tuple )

元組可以想成是一個嚴格的陣列，預先設定型別判定的陣列。

<br>

```
// 編譯前
let fufu: [string, number] = ['小富', 25];

// 編譯後
var fufu = ['小富', 25];
```

我們預先設定了陣列的型別判定，所以照著輸入的話沒有問題。

我們把值顛倒過來看看 ↓

```
let fufu: [string, number] = [25, '小富'];

// 會報錯
```

這個報錯主要是說在設定 `string` 的位置不能輸入 `number`；在設定 `number` 的位置不能輸入 `string`。

## 能不能只對其中一項賦值？

```
// 編譯前
let fufu: [string, number];
fufu[0] = '小富';

// 編譯後
var fufu;
fufu[0] = '小富';
```

元組是可以只對其中一項賦值的，但是僅能夠利用這種方式賦值。

```
let fufu: [string, number];
fufu = ['小富'];

// 會跳錯：Type '[string]' is not assignable to type '[string, number]'.
```

## 新增多的元素

當你設定只有兩個的話，並不能新增第三個元素進去。

```
let fufu: [string, number] = ['小富', 25, '小黃'];

// 會報錯：Type '[string, number, string]' is not assignable to type '[string, number]'.
```

但是如果是利用 `push()` 的方式就可以，不過只能是 `[string, number]` 其中一個型別。 ↓

```
// 編譯前
let fufu: [string, number] = ['小富', 25];
fufu.push('小黃');

// 編譯後
var fufu = ['小富', 25];
fufu.push('小黃');
```

```
let fufu: [string, number] = ['小富', 25];
fufu.push('小黃');
fufu.push(true);

// 會報錯： Argument of type 'boolean' is not assignable to parameter of type 'string | number'.
```

這個報錯主要是說：你只有能輸入 `string | number` 這兩種型別，你沒有定義說能使用 ` boolean` 這個型別。