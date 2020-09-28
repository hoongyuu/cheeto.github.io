---
title: JavaScript核心篇：箭頭函式
date: 2020-03-15 21:05:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 箭頭函式

```
let callName = function (someone) {
    return '我是 ' + someone
};
console.log(callName('小明')); // 我是 小明
```

轉成 箭頭函式語法 ↓ ↓ ↓

```
let callName = (someone) => '我是 ' + someone;
console.log(callName('小明')); // 我是 小明
```

當箭頭函式的程式碼為表達式時，不加 `{}` 的時候會自動加上 `return`，且只有一行時可以不加 `{}` 。

<br>

如果只有一個參數的時候還可以縮寫 ↓ ↓ ↓

```
let callName = someone => '我是 ' + someone;
console.log(callName('小明')); // 我是 小明
```

當只有一個參數時可以把參數的括號省略，如果 **沒有參數** 或 **多個參數** 時括號是不能省略的。


## 箭頭函式與傳統函式的不同之處

### 箭頭函式沒有 `arguments` 這個參數

```
let nums = function () {
    console.log(arguments)
};

nums(10, 50, 100, 50, 5, 1, 1, 1, 500);
```

會顯示一個類陣列 ↓ ↓ ↓

![箭頭函式-1](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%AE%AD%E9%A0%AD%E5%87%BD%E5%BC%8F-1.jpg?alt=media&token=bafb732a-87cb-4961-ab04-e53835e3876d)

那如果是箭頭函式 ↓

```
let nums = () => {
    console.log(arguments)
};

nums(10, 50, 100, 50, 5, 1, 1, 1, 500); 
// arguments is not defined at nums
```

它會回傳一個錯誤

### `this` 綁定的差異

箭頭函式沒有自己的 `this`

```
var myName = '全域';
var person = {
    myName: '小明',
    callName: function (){
        console.log('1', this.myName); // 1 小明
        setTimeout(function (){
            console.log('2', this.myName); // 2 全域
            console.log('3', this); // 3 window
        }, 10);
    }
};
```

但是如果用箭頭函式會變得有些不同哦 ↓

```
var myName = '全域';
var person = {
    myName: '小明',
    callName: function (){
        console.log('1', this.myName); // 1 小明
        setTimeout(() => {
            console.log('2', this.myName); // 2 小明
            console.log('3', this); // 3 callName
        }, 10);
    }
};

person.callName()
```

![箭頭函式-2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%AE%AD%E9%A0%AD%E5%87%BD%E5%BC%8F-2.jpg?alt=media&token=47ef310c-2f73-48aa-ad9b-af7bb8fb8330)

這邊因為箭頭函式沒有自己的 `this`，所以它會向外尋找，所以我們用 `person.callName()` 宣告的話，`this` 會指向 `person`。

<br>

如果我們把全部函式都換成箭頭函式呢？

```
var myName = '全域';
var person = {
    myName: '小明',
    callName: () => {
        console.log('1', this.myName); // 1 全域
        setTimeout(() => {
            console.log('2', this.myName); // 2 全域
            console.log('3', this); // 3 window
        }, 10);
    }
};
```

因為箭頭函式沒有自己的 `this`，所以它會一層一層向外找，直到找到 `window` 為止。


### `this` 不同，導致 DOM 的 `this` 也會指向不同位置

```
// HTML環境
<p>這裡具有一段話</p>


// JS
const ele = document.querySelector('p');
ele.addEventListener('click', function () {
    console.log(this)
});
```

這邊如果點擊 `p` 的話會顯示 `<p>這裡具有一段話</p>`

如果我們換成箭頭函式 ↓

```
// HTML環境
<p>這裡具有一段話</p>


// JS
const ele = document.querySelector('p');
ele.addEventListener('click', () => {
    console.log(this)
});
```

點擊 `p` 的話會顯示 `window`。

因為箭頭函式並沒有自己的 `this`，所以它就會指向 `window`。


### 無法透過 `call`, `apply`, `bind` 重新給予 `this`

```
const family = {
  myName: '小明家',
}
const fn = (para1, para2) =>  {
  console.log(this, para1, para2);
}
fn.call(family, '小明', '杰倫');
```

會顯示 ↓

![箭頭函式-3](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%AE%AD%E9%A0%AD%E5%87%BD%E5%BC%8F-3.jpg?alt=media&token=01cbb647-66d9-46e5-9504-299ff7265f6b)

可以發現就算用 `call` 去指定 `this` 也是沒有效果的。


### 箭頭函是 沒有 `prototype`

```
const Fn = function (a) {
  this.name = a;
};

const ArrowFn = (a) => {
  this.name = a;
};

console.log(Fn.prototype);
console.log(ArrowFn.prototype);
```

會顯示 ↓

![箭頭函式-4](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%AE%AD%E9%A0%AD%E5%87%BD%E5%BC%8F-4.jpg?alt=media&token=ba058278-ba6e-410a-9742-aa962fce956a)


如果要建構**實體**呢？

```
const Fn = function (a) {
  this.name = a;
};

const ArrowFn = (a) => {
  this.name = a;
};

const a = new Fn('a');
console.log(a);

const b = new ArrowFn('b');
```

![箭頭函式-5](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%AE%AD%E9%A0%AD%E5%87%BD%E5%BC%8F-5.jpg?alt=media&token=02d8cd10-b048-46e4-b456-4b68a46ed949)

這邊會發現箭頭函式是沒有辦法建構實體的，因為它本身並沒有 `prototype`。

所以箭頭函式是沒有辦法作為建構函式來使用的！！！


## 箭頭函式常見問題


前面的章節我們有說到如果不加 `{}` 的時候，會自動加上 `return` 。

```
const arrFn = () => 1; 
console.log(arrFn()); // 1
```

那如果我們要回傳的是一個物件呢？

```
const arrFn = () => {data: 1}; 
console.log(arrFn()); // undefined
```

這邊是會回傳一個 `undefined`。

解決方法 ↓

```
const arrFn = () => ({data: 1}); 
console.log(arrFn()); // {data: 1}
```

這樣就能夠順利回傳一個物件囉。


### 如果遇到判斷的情況

```
let num = 0;

const numFn = num || function (){return 1};
console.log(numFn());  // 1
```

那如果換成箭頭函式 ↓ ↓ ↓

```
let num = 0;

const numFn = num || () => 1;
console.log(numFn());  // 這邊會跳錯
```

解決方法 ↓

```
let num = 0;

const numFn = num || (() => 1);
console.log(numFn());  // 1
```

解決方法就是在外面包一個括號就能夠搞定囉！