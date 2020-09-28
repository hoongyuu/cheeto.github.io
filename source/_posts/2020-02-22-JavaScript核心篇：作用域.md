---
title: JavaScript核心篇：作用域
date: 2020-02-22 19:10:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---

# JavaScript 作用域

JavaScript是採用**語法作用域**，屬於**靜態作用域**的，靜態作用域是變數的作用域在語法解析的時候，就已經確定它的作用域了，確定完就無法再改變。

![作用域](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E4%BD%9C%E7%94%A8%E5%9F%9F.jpg?alt=media&token=ba25abbc-e1e6-4424-b859-031a5e7dd9fd)

如果作用域裡找不到變數的時候，就會向外查找，找不到的時候就會報錯(not define)。

<!--more-->

```
let value = 1
function num1(){
    console.log(value); // 1
}
function num2(){
    let value = 2;
    num1();
}
num2();  // console.log 顯示 1
```

以上方為例，num1 找 value 時會往外層全域尋找，但是有一點非常的重要，就是它尋找的時候不會跟執行環境有任何的關聯性，因為JavaScript是語法作用域，在程式碼撰寫的時候就已經確定了它的作用域。num2 裡面的 value 作用域就只有在 num2 的函式裡面，所以不會影響到外面全域變數的 value 。

<br/>

但是如果把 num2 變成下面這樣

```
let value = 1
function num1(){
    console.log(value); // 1
}
function num2(){
    value = 2;
    num1();
}
num2();  // console.log 顯示 2
```

那 num2 的 value 就會影響到外面的變數，所以顯示就會變成 2。