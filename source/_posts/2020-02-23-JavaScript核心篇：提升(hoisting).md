---
title: JavaScript核心篇：提升(hoisting)
date: 2020-02-23 19:16:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---

# 提升(hoisting)

在 JavaScript 當中 var 會有提升的效果出現，也可以說它是在創造階段就先把所有變數先宣告出來，接著再一一的賦予值進去。 舉例如下

```
var name = 'Cheeto';

//可以拆解成 ↓


// 創造階段
var name;
// 執行階段
name = 'Cheeto';
```
<!--more-->
### 函式陳述式(hoisting)

函式陳述式會完整的提升，再最開始創造階段的時候就會先把函式完整創造出來了。

```
function callName(){
    console.log('call Cheeto')
}
callName(); // 會正常顯示 call Cheeto


// 如果我們把 callName() 往上放呢？ 如下 ↓


callName(); // 一樣會正常顯示 call Cheeto
function callName(){
    console.log('call Cheeto')
}
```

原因是因為 callName 在最一開始讀取檔案的時候就在創造階段完整的讀取了，所以就算在函式的上方呼叫也會執行。

### 提升順序

在創造階段時，函式是最優先被創造的。

```
function callName(){
    console.log('呼叫小明1')
}
var callName = function (){
    console.log('呼叫小明2')
}

callName(); // 呼叫小明2

或是

var callName = function (){
    console.log('呼叫小明2')
}
function callName(){
    console.log('呼叫小明1')
}

callName(); //  一樣都會顯示 呼叫小明2
```

原因就是因為函式是會被最優先創造的，不管輸入順序如何執行順序都會如下

```
// 創造環境
function callName(){
    console.log('呼叫小明1')
}
var callName;
callName = function (){
    console.log('呼叫小明2')
}
// 執行環境
callName(); // '呼叫小明2'
```