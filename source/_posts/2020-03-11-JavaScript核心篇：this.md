---
title: JavaScript核心篇：this (合併整理)
date: 2020-03-11 21:44:12
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# this

* 每個執行環境都有屬於自己的 this 關鍵字
* this 與函式如何宣告**沒有關聯性**，僅與呼叫方式有關
* 嚴格模式下，簡易呼叫會有很大個改變

`this`的實際指向跟我們如何去呼叫函式是有很大的關聯性的！

`this`指的並不是函式本身，而是指向**目前呼叫函式或方法的擁有者(owner)物件**。所以函式需要了解函式的幾種調用方式，就能一併了解`this`在這些情況下的不同。

![影響函式this的調用方式](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%BD%B1%E9%9F%BF%E5%87%BD%E5%BC%8F%20this%20%E7%9A%84%E8%AA%BF%E7%94%A8%E6%96%B9%E6%B3%95.jpg?alt=media&token=412fd868-72e1-44bc-b8ba-d8408447c684)


## this: 物件的方式調用(最常見)

* this 與函式如何宣告**沒有關聯性**，僅與呼叫方式有關
* 物件方法調用時，僅需要關注是在哪一個物件下呼叫

![this的用途](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fthis%E7%9A%84%E7%94%A8%E9%80%94.jpg?alt=media&token=faaa2adc-6ab5-45f7-b3f2-3782119860fd)

```
function callName(e) {
    console.log(this, this.myName);
};

var family = {
    myName: '小明家',
    callName: callName,
    Ming: {
        myName: '小明',
        callName: callName
    }
}
family.callName();
family.Ming.callName();
```

![this 的常用方式](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fthis%E7%9A%84%E5%B8%B8%E7%94%A8%E6%96%B9%E5%BC%8F.jpg?alt=media&token=9e5acc26-1087-4072-85dc-a851b39ad0b4)

物件方法調用時，僅需要關注是在哪一個物件下呼叫。
所以`family.callName();`的`this`就是指向`family`；而`family.Ming.callName();`的`this`就是指向`family.Ming`。

```
var myName = '真心鎮大冒險';

function callName(e) {
    console.log(this, this.myName);
};

var family = {
    myName: '小明家',
    callName: function(){
        console.log(this.myName);
    }
}

var callName = family.callName;
callName();  // 真心鎮大冒險
```

`this` 與函式如何宣告**沒有關聯性**，僅與呼叫方式有關。

所以我們只要管它是如何被呼叫出來的就好，而 `callName()` 是在全域裡面被執行出來的，所以它的`this` 就會指向 `window`。


## this: 簡易呼叫(simple call)

* 盡可能不要使用 simple call 的 `this`

**簡易呼叫的 `this` 都會指向 window**
**簡易呼叫的 `this` 都會指向 window**
**簡易呼叫的 `this` 都會指向 window**

```
var myName = '真心鎮大冒險';

function callName(){
    console.log(this.myName);
}

callName();  // 真心鎮大冒險
```

原因是因為我們在全域呼叫函式，所以函式的 `this` 會指向 `window`，所以會指到全域變數的 myName。

而這種直接在全域下呼叫的方式就算是「簡易呼叫」的一種。


```
var myName = '真心鎮大冒險';

// IIFE 立即函式
(function (){
    console.log(this.myName); //真心鎮大冒險
    function callSomeone(){
        console.log(this.myName);
    }
    callSomeone(); //真心鎮大冒險
})()
```

this 不會看你的呼叫位置，而是依據呼叫方式而定的。

### 簡易呼叫(閉包)

```
var myName = '真心鎮大冒險';

function easyCard(base) {
    var money = base;
    var name = '悠遊卡';
    return function (update) {
        money = money + update;
        console.log(this.myName, money);
    }
}
var MingEasyCard = easyCard(100);
MingEasyCard(10);  // 真心鎮大冒險 110
```

這邊也可以看到它跟前面的例子一樣都是在全域下直接呼叫，所以它的`this`就是指向 window。

### 簡易呼叫(callback)

所謂的「Callback function」其實就是「把函式當作另一個函式的參數，透過另一個函式來呼叫它」。

以`callback function` 的方式被呼叫，所以算是「簡易呼叫」。所以 `this` 會指向 window。

```
var myName = '真心鎮大冒險';

function myEasyCard(callback) {
    var money = 100
    return callback(money)
}
myEasyCard(function (money) {
    console.log(this.myName, money + 100)
});
```

![callback範例](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fcallback%E7%AF%84%E4%BE%8B.jpg?alt=media&token=2b15683c-8378-43d7-920b-01b239a26dbf)

<br>

再來下一個範例

```
var myName = '真心鎮大冒險';

var family = {
    myName: '小明家',
    callName: function () {
        setTimeout(function () {
            console.log(this.myName);
        }, 1000);
    }
}
family.callName();  //真心鎮大冒險
```
`this` 不會看你是在那裡執行，而是看你是如何去執行它。因為`setTimeout`的()內是一個`callback function`，所以它是以`callback function` 的方式被呼叫，所以算是「簡易呼叫」。


<br>

如果想要把 `this` 指向 `family` 的話，解決方法如下 ↓

```
var family = {
myName: '小明家',
callName: function () {
    var self = this; // vm, that
    setTimeout(function () {
      console.log(self.myName);
    }, 1000);
  }
}
family.callName(); //小明家
```
## this： call, apply, bind 

### call

```
var family = {
    name: '小明家'
};

var fn = function (para1, para2) {
    console.log(this, para1, para2);
};
fn('小明', '杰倫');
fn.call(family, '小明', '杰倫');
```

![call](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fcall.jpg?alt=media&token=c6d6b156-5f64-4a2f-a5a9-29054464481c)

`call`的語法是能夠把 `family` 傳入 `this` 當中，這樣就能指定自己要的`this`

### apply

```
var family = {
    name: '小明家'
};

var fn = function (para1, para2) {
    console.log(this, para1, para2);
};
fn.call(family, '小明', '杰倫');
fn.apply(family, ['小明', '杰倫']);
```

![apply](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fapply6.jpg?alt=media&token=d8dbb732-8310-4052-9b50-4c840262f9da)

`apply`的語法其實跟`call`滿相近的，但是它後面的參數必須用陣列的方式設定。

### bind

`bind`的語法跟`call`是一樣的方式，但是兩者的不同在於說：「`bind`不會被立刻地執行」

```
var family = {
    name: '小明家'
};

var fn = function (para1, para2) {
    console.log(this, para1, para2);
};
fn.call(family, '小明', '杰倫');
fn.bind(family, '小明', '杰倫');
```

這裡如果執行的話只會出現 `fn.call(family, '小明', '杰倫');` 的結果，而`bind`的執行結果不會出現。

因為「`bind`不會被立刻地執行」

```
var family = {
    name: '小明家'
};

var fn = function (para1, para2) {
    console.log(this, para1, para2);
};
fn.call(family, '小明', '杰倫');
var fn2 = fn.bind(family, '小明', '杰倫');
fn2();
```

![apply](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fapply6.jpg?alt=media&token=d8dbb732-8310-4052-9b50-4c840262f9da)

### call, apply, bind 進階觀念

以`call`, `apply`, `bind`呼叫函式時，**可以綁定`this`是什麼。`this`會是傳進該函式的第一個參數。**

`call`, `apply`, `bind`**在非嚴格的模式下，`null`, `undefined`會被置換成全域變數**，而原生型態的值將會被物件包裹呈現

如果把`this`傳入純值的話，會用物件包裹的方式呈現。

```
var fn = function (para1, para2) {
    console.log(this, para1, para2);
};
fn.call(1, '小明', '杰倫');
fn.call('文字', '小明', '杰倫');
fn.call(true, '小明', '杰倫');
```

![this進階觀念](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fthis%E9%80%B2%E9%9A%8E%E8%A7%80%E5%BF%B5.jpg?alt=media&token=6c1e2b67-148b-4c02-a6fa-b13b9dc24e04)


## 嚴格模式(Strict Mode)

![嚴格模式](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%9A%B4%E6%A0%BC%E6%A8%A1%E5%BC%8F.JPG?alt=media&token=a8478f9a-7845-4d7a-b030-66e3f404e77e)

* 在嚴格模式下未定義的變數不能直接的賦予值

```
(function () {
    'use strict';
    auntie = '漂亮阿姨';
    // Uncaught ReferenceError: auntie is not defined
})();
```

* 嚴格模式對`this`的影響

```
function callStrict(para1, para2) {
    'use strict';
    console.log(this, typeof this, para1, para2);
}
callStrict.call(1, '小明', '杰倫')
callStrict.call(undefined, '小明', '杰倫')
callStrict('小明', '杰倫')
```

![嚴格模式this](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%9A%B4%E6%A0%BC%E6%A8%A1%E5%BC%8Fthis.jpg?alt=media&token=8748a537-c086-46fa-980e-0a57083ed509)


simple call的`this`沒有設定的話預設會是`undefined`，但是在非嚴格模式的時候會被轉成`object`，然而在嚴格模式下它並不會轉化，依舊會維持本來的`undefined`，所以**盡可能不要使用簡易呼叫的`this`**！！！

## this: DOM

DOM跟`this`綁定會讓`this`指向觸發事件的元素(HTML element)。

```
<button onclick="console.dir(this)">按鈕</button>
```

![thisDOM範例一](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2FthisDOM%E7%AF%84%E4%BE%8B%E4%B8%80.jpg?alt=media&token=6cafe677-d0a5-4e10-81de-c07e480219bf)

這裡`onclick`事件裡的`this`，就是指向`button`的元素。


```
var fn = function () {
    console.dir(this);
    this.style.backgroundColor = 'orange';
};

var els = document.querySelectorAll('li');

for (let i = 0; i < els.length; i++) {
    els[i].addEventListener('click', fn, false);
};
```

![thisDOM範例二](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2FthisDOM%E7%AF%84%E4%BE%8B%E4%BA%8C.jpg?alt=media&token=9924ff20-5694-4a0c-882c-6201f32ff393)

DOM的事件監聽會讓`this`指向觸發事件的元素(HTML element)。