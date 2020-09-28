---
title: JavaScript核心篇：執行緒 與 同步、非同步
date: 2020-02-24 18:32:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---

## 執行緒

JavaScript 是一個單執行緒的程式，

![單執行緒](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%96%AE%E5%9F%B7%E8%A1%8C%E7%B7%92%E7%90%86%E8%A7%A3.jpg?alt=media&token=846b63c1-c45d-464f-8dc6-ea44ffeefae1)

單執行緒是沒有辦法把任務一次全部執行，如上圖所示，它必須先完成 '吃早餐' 接著 '打給漂亮阿姨' 再來才是 '洗碗'。

## 同步、非同步

同步的任務是依序執行，不會一個任務還沒有完全的執行完畢就跳到下一個任務。

非同步如下

```
function eatBreakfast(e) {
    console.log('吃早餐');
};

function callSomeone(someone) {
    console.log('打給' + someone);

    // 這段程式碼是非同步的任務，會先移動到事件佇列
    setTimeout(function (e) {
      console.log(someone + '回電');
    }, 2000);
};

function washingPlate(e) {
    console.log('洗碗盤');
};

function doWork(e) {
    let auntie = '漂亮阿姨';

    eatBreakfast();
    callSomeone(auntie);
    washingPlate();
};

doWork()
```

JavaScript 會把非同步的任務放到**事件佇列**裡面，如下圖所示。
在 doWork 中依序執行了
1. 吃早餐
2. 打給漂亮阿姨
3. 洗碗盤

但是在打給漂亮阿姨的時候它會先偵測到裡面的非同步任務，就會把非同步任務丟到時間佇列，等到 doWork() 全部執行完了才會把事件佇列裡的任務執行。

![非同步執行](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E9%9D%9E%E5%90%8C%E6%AD%A5%E5%9F%B7%E8%A1%8C%E7%A8%8B%E5%BA%8F.jpg?alt=media&token=98f1b478-1443-4e35-978c-4849e5d352a5)


**監聽事件也可以做到非同步**，如下 ↓

```
function clickTxt(e){
    console.log('點擊成功');
};

let txt = document.querySelecter('.txt');

// 這裡就是把 click 放到事件佇列裡面，等到我們點擊 txt 的時候才會執行 clickTxt 的函式
txt.addEventListener('click',clickTxt,false);
```