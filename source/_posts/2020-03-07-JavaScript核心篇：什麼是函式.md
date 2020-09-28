---
title: JavaScript核心篇：什麼是函式？
date: 2020-03-07 15:40:40
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 什麼是函式

```
function afunction(parameter) {
    var localVariable = '區域變數';
    console.log(this, localVariable); // This、區域變數

    return '附加一段' + parameter; // 回傳、參數
}
var data = afunction('參數');// 呼叫函式
console.log(data);
```

結果會呈現 ↓

![函式結構](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%87%BD%E5%BC%8F%E7%B5%90%E6%A7%8B.jpg?alt=media&token=ee48e915-6932-4110-a850-8d8cc82f4569)

function 有預設一個回傳的**值**，所以它能夠被當作表達式來用。

<!--more-->

<br>

當我們使用 `function` 去宣告一個字詞的時候，這個字詞就會變成一段函式，它就能夠有下列三種特性。

![什麼是函式](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E4%BB%80%E9%BA%BC%E6%98%AF%E5%87%BD%E5%BC%8F.jpg?alt=media&token=8b8a8324-d127-4eeb-8a2d-d15185c02c7c)

函式的名稱是選用的，意思就是可以有名稱也可以沒有，有名稱的稱為「**具名函式**」；沒名稱的稱為「**匿名函式**」。


## 函式 ( 陳述式、表達式 )

```
function functionA() {
    console.log('函式陳述式', '具名函式');
    console.log(functionA);
}
functionA();

var functionB = function() {
	console.log('函式表達式', '匿名函式');
	console.log(functionB);
}
functionB();
```

結果會呈現 ↓

![函式 ( 陳述式、表達式 )](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%87%BD%E5%BC%8F(%E9%99%B3%E8%BF%B0%E5%BC%8F%E3%80%81%E8%A1%A8%E9%81%94%E5%BC%8F).jpg?alt=media&token=a74c29eb-f405-4ddd-b26c-5bd9b854cd9e)


### 函式表達式也能用具名函式

用函式表達式也能夠使用具名函式，但是只能在函式內被調用。

```
var functionC = function functionD() {
     console.log(functionC ,functionD);
}
functionC();
console.log(functionD); // functionD is not defined
```

結果會呈現 ↓

![函式表達式(具名函式)](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%87%BD%E5%BC%8F%E8%A1%A8%E9%81%94%E5%BC%8F(%E5%85%B7%E5%90%8D%E5%87%BD%E5%BC%8F).jpg?alt=media&token=68368f28-92b7-4d51-90cd-08105eaf39de)

會 `not defined` 是因為，**函式表達式(具名函式)只能在函式內被調用！！！**