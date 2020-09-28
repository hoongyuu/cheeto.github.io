---
title: JavaScript核心篇：Getter 與 Setter，賦值運算不使用函式
date: 2020-03-15 14:20:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# Getter 與 Setter，賦值運算不使用函式

## setter - 存值的方法

```
var wallet = {
	total: 100,
	set save (price){
        this['total'] = this['total'] + price/2;
	}
};

wallet['save'] = 300;

console.log(wallet['total']);  // 250
```

`wallet['save'] = 300;` 這邊右邊的 300 會傳入 `price` 這個參數內。

這裡並不是用函式的方式來執行`setter`，而是用賦值的方式。

<!--more-->
<br>

## getter - 取得特定值的方法

`getter` 因為是取值的概念，所以不會傳入參數

```
var wallet = {
    total: 100,
    set save(price) {
    	this.total = this.total + price / 2;
    },
    get save() {
        // 因為是取值所以要加入 return
    	return this.total / 2;
    }
};

console.log(wallet.save);
wallet.save = 300;
console.log(wallet);
```

![Getter 與 Setter-1](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fgetter%E8%88%87setter-1.jpg?alt=media&token=99a805f6-ec8f-460f-9019-ff8ead5275b6)



## 利用 `Object.defineProperty()` 來定義 Getter 與 Setter 

除了上述的方法之外，利用`Object.defineProperty()`也能夠設定 Getter 與 Setter。

```
var wallet = {
    total: 100,
};

Object.defineProperty(wallet, 'save', {
    set: function (price) {
    	this.total = this.total + price / 2;
    },
    get: function () {
    	return this.total / 2;
    }
})
```

![Getter 與 Setter-2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fgetter%E8%88%87setter-2.jpg?alt=media&token=a89070aa-ab15-4a7e-a759-b422cf5e2d9b)

可以發現被紅色框框所框起來的地方顏色變了，這是因為屬性特徵上用`defineProperty`定義出來它預設會是：`不可刪除`、`不可列舉`

```
// 後面加上這組程式碼來驗證看看
console.log(Object.getOwnPropertyDescriptor(wallet, 'save'));
```

![Getter 與 Setter-3](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fgetter%E8%88%87setter-3.jpg?alt=media&token=7e1d677a-0313-43f4-91d9-019037046e29)


那這邊也有解決方法 ↓ ↓ ↓

```
var wallet = {
    total: 100,
};

Object.defineProperty(wallet, 'save', {
    configurable: true,
    enumerable: true,
    set: function (price) {
    	this.total = this.total + price / 2;
    },
    get: function () {
    	return this.total / 2;
    }
})
```

![Getter 與 Setter-4](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Fgetter%E8%88%87setter-4.jpg?alt=media&token=312a2b6c-a031-4c92-9e58-1907b1f638e0)

只要利用 `defineProperty` 把屬性特徵定義成「**可以刪除**」、「**可以列舉**」這樣就沒問題了，可以發現 `save` 的顏色也變回來了。