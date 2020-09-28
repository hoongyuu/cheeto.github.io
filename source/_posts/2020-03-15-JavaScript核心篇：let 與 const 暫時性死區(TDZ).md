---
title: JavaScript核心篇：let 與 const 暫時性死區(TDZ)
date: 2020-03-15 17:40:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# let 與 const 暫時性死區(TDZ)

1. let 一樣會有創造階段
2. 但是從創造到執行階段會出現**暫時性死區**(TDZ)，這個區域無法呼叫該變數
3. 有創造到執行的概念，但是它不會預先出現 `undefined` 而是會跳出 `Error`

> 文件不會表明這與 `var` 的 `hoisting` 相同

<!--more-->

```
{
console.log(Ming);
let Ming = '杰倫';
}
```

這邊會跳出錯誤 ↓

![let 與 const 暫時性死區-1](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Flet%2Cconst%E6%9A%AB%E6%99%82%E6%80%A7%E6%AD%BB%E5%8D%80-1.jpg?alt=media&token=f55f3b26-ce9b-4e25-a8f8-622aa44ae730)

在裡面其實它的執行是這樣的 ↓ ↓ ↓

```
// 創造階段
let Ming; // 暫時性死區(TDZ)，無法呼叫

// 執行階段
console.log(Ming);
Ming = '杰倫';
```


接下來看下一個範例

```
console.log(typeof a);
console.log(typeof myName);

let myName = '';
```

來看看差別在哪裡 ↓ ↓ ↓

![let 與 const 暫時性死區-2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Flet%2Cconst%E6%9A%AB%E6%99%82%E6%80%A7%E6%AD%BB%E5%8D%80-2.jpg?alt=media&token=fd59b785-b0e1-41d0-add4-5f33ec0f5a22)


這邊可以看到我們並沒有辦法在 `let` 宣告之前去取得它，就算是 `typeof` 也是會跳錯的哦！