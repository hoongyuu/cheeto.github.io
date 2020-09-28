---
title: JavaScript核心篇：閉包
date: 2020-03-10 16:57:12
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 閉包

```
function storeMoney() {
    var money = 500;
    return function (price) {
        money = money + price;
        return money
    }
};
var mingMoney = storeMoney();
console.log(mingMoney(50)); // 550
console.log(mingMoney(50)); // 600
console.log(mingMoney(50)); // 650
```

這邊可以發現 `mingMoney` 的值有繼續被增加，原因是實際上釋放記憶體的條件是「當變數無法被引用時就會釋放記憶體」，而現在這個函式被綁定在全域變數上，所以它能夠不斷的呼叫，所以記憶體並不會被釋放。

<br>

再來看下一個範例

```
function storeMoney() {
    var money = 500;
    return function (price) {
        money = money + price;
        return money
    }
};
var mingMoney = storeMoney();
console.log(mingMoney(50)); // 550
console.log(mingMoney(50)); // 600
console.log(mingMoney(50)); // 650

var jayMoney = storeMoney();
console.log(jayMoney(1000)); // 1500
console.log(jayMoney(1000)); // 2500
console.log(jayMoney(1000)); // 3500
```

這裡兩個變數各自呼叫了函式，所以它們會有各自的回傳結果。

也可以想成每次回傳都生成一個新的位址。


## 閉包申論

```
function arrFunction(e) {
    var arr = [];
    for (var i = 0; i < 3; i++) {
        arr.push(function (e) {
            console.log(i);
        });
    }
    console.log('i = '+ i);
    return arr;
}

var fn = arrFunction();
fn[0]();  
fn[1]();  
fn[2](); 
```

![閉包申論](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E9%96%89%E5%8C%85%E7%94%B3%E8%AB%96.jpg?alt=media&token=1dfc3b52-18c3-4b2a-a201-3ae5842f8925)

會造成全部都出現 3 是因為 `var` 的作用域是在 `function` 內，所以它會汙染到 `for` 外面的 `i` 。


解決方法很簡單 ↓

```
function arrFunction(e) {
    var arr = [];
    for (let i = 0; i < 3; i++) {
        arr.push(function (e) {
            console.log(i);
        });
    }
    //console.log('i = '+ i); // 如果有這層程式碼會報錯，因為找不到 i 變數
    return arr;
}

var fn = arrFunction();
fn[0]();  // 0
fn[1]();  // 1
fn[2]();  // 2
```

因為 `let` 的作用域是限制在 `{}`，所以在 `for` 就已經把它限制住了。


## 閉包工廠

```
function storeMoney(initValue) {
    var money = initValue || 500;
    return function (price) {
        money = money + price;
        return money
    }
};

var mingMoney = storeMoney(100); // 起始 100
console.log(mingMoney(500));  // 增加 500
```

這裡利用了 `var money = initValue || 500;` 來做出預設值。
 
## 私有方法

```
function storeMoney(initValue) {
    var money = initValue || 500;
    return {
        increase: function (price) {
            money += price;
        },
        decrease: function (price) {
            money -= price;
        },
        nowMoney: function (price) {
            return money;
        }
    };
};

var mingMoney = storeMoney(100); // 起始 100
mingMoney.increase(100);    // 起始 100 + 100 = 200
mingMoney.increase(100);    // 200 + 100 = 300
mingMoney.decrease(50);    // 300 - 50 = 250
mingMoney.decrease(25);    // 250 - 25 = 225
console.log(mingMoney.nowMoney()); // 最後會顯示 225
```

這是可以在回傳的時候加入一個物件，利用物件去做加減的運算。
