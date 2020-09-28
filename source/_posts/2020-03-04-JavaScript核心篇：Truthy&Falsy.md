---
title: JavaScript核心篇：Truthy&Falsy
date: 2020-03-04 13:57:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# Truthy Falsy

在 JavaScript 中，truthy(真值) 指的是在布林值判斷中，轉換後的值為真的值。我們也可以另外一個方向來理解「除了 falsy 以外的值都是 truthy」，那我們就可以來看看 falsy 的值有哪些了。如下

* 0
* NaN
* '' (空字串)
* false
* null
* undefined

![Truthy Falsy](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Ftruthy%26falsy.jpg?alt=media&token=a1723750-2d5b-49f3-8ef7-8c007eb3c73f)

<!--more-->

以下列程式碼為例

```
if (){
    console.log('執行程式');
}else{
    console.log('執行 falsy');
}
```

在 if 的 () 當中輸入 falsy 的六種值，都會出現 '執行 falsy' 的訊息。


## 包裹物件轉化

如果我們使用了物件包裹，那就是另外一回事了！

```
if (new Number(0)){
    console.log('執行程式'); // 會顯示這邊
}else{
    console.log('執行 falsy');
}
```

這裡可以看到我們利用包裹物件來把 0 轉化，它會變成 truthy。

```
if (new Boolean(false)){
    console.log('執行程式'); // 一樣會顯示這邊
}else{
    console.log('執行 falsy');
}
```

答案是因為利用包裹物件轉化的值都會變成物件，物件裡不管是什麼值都會回傳 true。

![包裹物件轉化](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Ftruthy%E5%8C%85%E8%A3%B9%E7%89%A9%E4%BB%B6%E8%BD%89%E5%8C%96.jpg?alt=media&token=bc21934c-c7da-4557-bcb3-e4bef5952881)