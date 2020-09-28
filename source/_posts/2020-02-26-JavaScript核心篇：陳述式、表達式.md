---
title: JavaScript核心篇：陳述式(Statement)、表達式(Expression)
date: 2020-02-26 21:37:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---



## 陳述式 (Statement)

**陳述式一定會做一些事情，但陳述式不會產生(回傳)數值**。所以不能被放在 JS 內預期會產生數值的地方。

什麼意思是不能被放在 JS 內預期會產生數值的地方呢？

```
    var a = if(){
        var b = 5
        console.log(b)
    }
    // 回傳 Uncaught SyntaxError: Unexpected token 'if'
```

因為 **if 是陳述式，所以它不會回傳值**。

下列都是 JavaScript 的陳述式：

1. 變數宣告
2. if 判斷式
3. while 迴圈
4. for 迴圈
5. switch 迴圈
6. 函式陳述式

上面的這些都是陳述式，這些程式碼都會執行某些動作，但是它們都有一個共通的特性，那就是不會回傳一個值給你。

這裡有一點要注意

```
// 區塊陳述 (Block Statement)
{
    var name = 'Cheeto';
}

// 物件實字
{
    name: 'Cheeto';
}
```

這邊如果宣告

```
var a = {
    var name = 'Cheeto';
}
// 會跳錯，因為區塊陳述跟if區塊一樣，執行完成後都不會回傳一個值
```

而**物件實字則是會回傳**。

<br/>


## 表達式(Expression)

表達式會回傳一個值，且很常是運算式。

>表達式是一段 JS 直譯器能夠運算並產生數值的程式碼。

![表達式](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E8%A1%A8%E9%81%94%E5%BC%8F.jpg?alt=media&token=eefa735e-125e-45c0-9e1a-df12e3c91739)

可以發現上圖這些程式碼都會回傳一個值，所以這些都是表達式。

## 函式陳述式、函式表達式

兩者差別在於 hoisting 的不同。提升章節有說到。

```
// 函式陳述式、具名函式
function callName(){
    ...
}

// 函式表達式、匿名函式
var callName = function (){
    ...
}
```