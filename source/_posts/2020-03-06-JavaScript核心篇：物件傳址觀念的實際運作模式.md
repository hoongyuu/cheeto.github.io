---
title: JavaScript核心篇：物件傳址觀念的實際運作模式
date: 2020-03-06 13:50:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 物件傳址觀念的實際運作模式

在這篇章節來實做看看傳址的運作模式，由下面的程式碼為範例。

```
var a = {x: 1};
var b = a;
a.y = a = {x: 2};
console.log(a.y);
console.log(b);
```

接下來就一步一步的來看看傳址的運作邏輯吧！

<!--more-->

## 第一步驟

```
var a = {x: 1};
var b = a;
```

![傳址第一步驟](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%82%B3%E5%9D%80%E7%AC%AC%E4%B8%80%E6%AD%A5%E9%A9%9F.jpg?alt=media&token=31b2216e-0374-40f6-9d7c-d9d8a9623a1b)

因為物件型別是傳址的特性，所以 `var b = a;` 時是指向同一個位址。


## 第二步驟

```
a.y = a = {x: 2};
```

![傳址第二步驟](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%82%B3%E5%9D%80%E7%AC%AC%E4%BA%8C%E6%AD%A5%E9%A9%9F.jpg?alt=media&token=0ae02b66-c688-44ce-bfba-9d15bb6ee04d)

雖然 =(等號) 的[相依性](https://hoongyuu.github.io/cheeto.github.io/2020/03/02/2020-03-02-JavaScript%E6%A0%B8%E5%BF%83%E7%AF%87%EF%BC%9A%E5%84%AA%E5%85%88%E6%80%A7%E3%80%81%E7%9B%B8%E4%BE%9D%E6%80%A7/)是由右至左，但`a.y = a = {x: 2};`是同時運行的，所以 `a.y` 和 `a` 都會指向同一個位址。

## 最後

```
console.log(a.y);
console.log(b);
```

這邊可以由第二步驟看到，由於 `a` 已經指向 `0x02` 的位址，裡面並沒有 `y` 這個屬性，所以會回傳 undefined。
而第二步驟時 `a.y = a = {x: 2};` 裡面的 `a.y = {x: 2};` 其實也可以等於 `b.y = {x: 2};`，因為它們在這時還是同一個參考位址。

所以就會產生下列這樣的結果 ↓

![物件運作測試](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%89%A9%E4%BB%B6%E9%81%8B%E4%BD%9C%E6%B8%AC%E8%A9%A6.jpg?alt=media&token=d99fcb34-44a3-4352-8291-4bc7d87e5f7c)
