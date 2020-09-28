---
title: JavaScript核心篇：立即函式
date: 2020-03-08 16:42:40
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 立即函式

立即函式有幾個特點：
1. 立刻執行
2. 無法在函式外被再次執行


## 語法

一般的函式是這樣子寫的

```
function IIFE(){
    console.log('立即函式：簡稱 "IIFE"');
}
```

那立即函式的語法就像這樣 ↓

```
(function IIFE(){
    console.log('立即函式：簡稱 "IIFE"');
}());

或

(function IIFE(){
    console.log('立即函式：簡稱 "IIFE"');
})();
```


如果我們再次把它叫出來會發生什麼事呢？

```
(function IIFE(){
    console.log('立即函式：簡稱 "IIFE"');
}());
IIFE();
```

呈現結果 ↓

![立即函式再次呼叫](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%AB%8B%E5%8D%B3%E5%87%BD%E5%BC%8F%E5%86%8D%E6%AC%A1%E5%AE%A3%E5%91%8A.jpg?alt=media&token=d2f596a5-2ae1-4793-92ac-cee20cc0fae9)

因為立即函式**無法在函式外被再次執行**


<br>

立即函式就算不給它名稱也能夠執行，大部分的立即函式都不需要名稱的。

```
(function (){
    console.log('立即函式：簡稱 "IIFE"');
}());

//把函式內的括號放到外面也能夠執行

(function (){
    console.log('把函式內的括號放到外面也能夠執行');
})();
```

![立即函式名稱問題](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%AB%8B%E5%8D%B3%E5%87%BD%E5%BC%8F%E5%90%8D%E7%A8%B1%E5%95%8F%E9%A1%8C.jpg?alt=media&token=089bb9fc-1e96-42d6-9dc0-90e5f09edc56)


## 立即函式用途

1. 限制變數的作用域

```
(function (){
    var Ming = '小明';
    console.log(Ming); //小明
})();
console.log(Ming); //not defined
```

2. 可以帶入參數

```
(function (where){
    console.log(where)
})('小明在此');  // 回傳 '小明在此'
```

3. return 後可以帶入變數

```
var whereMing = (function (where) {
    console.log(where)
    return where;
})('小明在此'); // 回傳 '小明在此'

console.log(whereMing); // 回傳 '小明在此'
```

4. 立即函式間的傳遞

```
var a = {};
(function (b){
    b.name = '小明';
}(a));

(function (c){
    console.log(c.name); // 回傳 '小明'
}(a));
```