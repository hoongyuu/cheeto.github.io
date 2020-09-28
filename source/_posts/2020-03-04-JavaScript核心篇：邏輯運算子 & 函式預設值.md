---
title: JavaScript核心篇：邏輯運算子 & 函式預設值
date: 2020-03-04 16:51:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 邏輯運算子 & 函式預設值

![MDN範例](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fand%20or.jpg?alt=media&token=01509619-ecc9-4273-8abc-376130ac1431)

> [圖片取自 MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Expressions_and_Operators#%E9%82%8F%E8%BC%AF%E9%81%8B%E7%AE%97%E5%AD%90)

<!--more-->
 

## && (並且)

* 當第一個值為 falsy(假值)，就會直接回傳並且不會讀取第二個值。
* 當第一個值為 truthy(真值)，無論第二個值是 truthy(真值) 或是 falsy(假值)，都會回傳第二個值。

![&&回傳測試](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%26%26%E5%9B%9E%E5%82%B3%E6%B8%AC%E8%A9%A6.jpg?alt=media&token=4f2195f2-8ec9-4549-a2cd-db6472d41121)

## || (或者)

* 當第一個值為 truthy(真值)，就會直接回傳並且不會讀取第二個值。
* 當第一個值為 falsy(假值)，無論第二個值是 truthy(真值) 或是 falsy(假值)，都會回傳第二個值。

![||回傳測試](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2FOR%E5%9B%9E%E5%82%B3%E6%B8%AC%E8%A9%A6.jpg?alt=media&token=cf2cbf79-14d2-42cc-9b5e-08600069000f)


## ! (not)

! 就是否定的意思，只要 truthy(真值) 就會回傳 false，falsy(假值) 則會回傳 true

![!回傳測試](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fnot%E6%B8%AC%E8%A9%A6.jpg?alt=media&token=8cd0d59f-606f-4bd3-8827-cb7e24fad8c6)


## 函式預設值

```
var originCash = 500;
function updateEasyCard(cash){ 
    console.log(cash);
    var currentCash = originCash + cash;
    console.log('我有' + currentCash + '元');
}
updateEasyCard();
```

![函式預設值](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%87%BD%E5%BC%8F%E9%A0%90%E8%A8%AD%E5%80%BC01.jpg?alt=media&token=853ddb32-dbb3-47bc-8804-1162b1547d9e)

因為 `updateEasyCard();` 沒有定義給它一個數字，所以會是 undefined ，而 undefined 如果跟數字相加則會回傳 NaN。

<br>

這時候我們就可以用到剛剛學到的邏輯運算子了！

```
var originCash = 500;

function updateEasyCard(cash) {
    cash = cash || 500;
    console.log(cash);
    var currentCash = originCash + cash;
    console.log('我有' + currentCash + '元');
}
updateEasyCard();
```

記得上面的特性嗎？如果第一個為真值它會直接回傳，如果第一個值為假值就一定會回傳第二個值。所以這裡在沒有定義的時候會回傳 500。

![函式預設值](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%87%BD%E5%BC%8F%E9%A0%90%E8%A8%AD%E5%80%BC%2002.jpg?alt=media&token=f5fe251d-f700-438d-afd4-01a9db31094a)

<br>

但是這裡就有一個問題了，我如果輸入 updateEasyCard(0); 的話，因為 0 本來就是假值，所以它還是會回傳 500 ，那這時候就要換一種方式了。 解決方式如下 ↓

```
var originCash = 500;

function updateEasyCard(cash) {
    cash = parseInt(cash);
    cash = (cash || cash === 0) ? cash : 500;
    var currentCash = originCash + cash;
    console.log('我有' + currentCash + '元');
}
updateEasyCard(0);
```

這時候如果 (cash || cash === 0) 其中有一個是 true 的時候，就會回傳 cash 的值，否則回傳 500 。 這樣就解決了剛剛的問題囉！