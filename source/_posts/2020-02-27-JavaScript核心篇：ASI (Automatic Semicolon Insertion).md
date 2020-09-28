---
title: JavaScript核心篇：ASI (Automatic Semicolon Insertion)
date: 2020-02-27 21:39:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# ASI (Automatic Semicolon Insertion)

JavaScript 基本上在語句結尾時都要加上 ;(分號)，當語句沒有加入分號時，就會受到 ASI 的規則影響

ASI規則：當語法併到上一行的時候會出現錯誤時，它會自動加上 ;(分號)。

```
    function callName(){
      return 
      '叫我小明';
    }
    console.log(callName()); // undefined
```

會因為 ASI 的規則變成下面這樣

```
    function callName(){
      return; '叫我小明';
    }
    console.log(callName());
```

“不會” 發生 ASI 的規則：

1. 新的一行是 `(`、`[`、`/` 開始 (容易出錯的地方)

```
var a = 1
var b = a
(a + b).toString()
(function() { })()
(function() { })()
var a = 1
var b = a
/test/.test(b)
```

2. 新的一行以 `+`、`-`、`*`、`%` 作開始 (會影響執行結果)

```
var a = 2
var b = a
+a
```

3. 新的一行以 `,`、`.` 作開始 (需注意執行結果)

```
var a = 2
var b = a
.toString()
console.log(typeof b)
var a = 1
,b = 2 // b 一樣會 var 被宣告