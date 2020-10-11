---
title: TypeScript 從零開始：函式型別
date: 2020-09-23 21:20:00
tags:
  - TypeScript
categories: 
  - TypeScript
---

# TypeScript 從零開始：函式型別

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FXZBuk51.png?alt=media&token=190cc704-893e-4dea-ac8c-65043a94280d)

TypeScript 是 JavaScript 的超集合，將強型別帶入 JavaSript，並提供對 ES6 的支援，而 TypeScript 由 Microsoft 開發，程式開源於 **GitHub** 上。

> 學習資源參考 [TypeScript 新手指南](https://willh.gitbook.io/typescript-tutorial/)

<!--more-->

# 函式型別

這個章節主要會介紹到**函式表達式**、**函式陳述式**在 TS 當中是如何定義。

* 函式陳述式：

```
// 編譯前
function func1(num1: number, num2: number): number {
  return num1 + num2;
}

console.log(func1(2, 2));

// 編譯後
function func1(num1, num2) {
    return num1 + num2;
}
console.log(func1(2, 2));  // 4
```

首先要說參數裡面可以定義型別，那 `func1(...): number` 後面的這個 `number` 就是定義回傳值的型別。

* 函式表達式：

```
// 編譯前： 可以有兩種寫法
const func1 = (num1: number, num2: number): number => num1 + num2;
const func2: (num1: number, num2: number) => number = (num1, num2) => num1 + num2;

console.log(func1(2, 2));
console.log(func2(4, 4));

// 編譯後
var func1 = function (num1, num2) { return num1 + num2; };
var func2 = function (num1, num2) { return num1 + num2; };
console.log(func1(2, 2)); // 4
console.log(func2(4, 4)); // 8
```

## 可選參數

如果定義兩個參數就必須使用兩個，不能只使用一個。

```
const func1 = (num1: number, num2: number): number => num1;
console.log(func1(2));

// 會報錯：An argument for 'num2' was not provided.
```

那如果想要只用一個參數的話就可以設定**可選參數**啦！

```
// 編譯前
const func1 = (num1: number, num2?: number) => {
  if (num2) {
    return num1 + num2;
  } else {
    return num1;
  }
}
func1(2)

// 編譯後
var func1 = function (num1, num2) {
    if (num2) {
        return num1 + num2;
    }
    else {
        return num1;
    }
};
func1(2); // 2
```

這樣就知道可選參數如何設定了吧？

## 如何從 interface 中定義函式

```
// 編譯前
interface FuncTS {
  (num1: number, num2: number): number
}
const func1: FuncTS = (x, y) => x + y;
func1(5, 4);

// 編譯後
var func1 = function (x, y) { return x + y; };
func1(5, 4);
```

## 預設參數

在 ES6 之後有了預設參數，在 TS 當中當然也會有啦！

```
const animals = (type: string = '狗', color: string = '黑色', size: string = '大型') => {
  return `這隻${ type }毛色是 ${ color }，體型是 ${ size }`
}

animals('小貓', '灰色')
```

方法就跟 ES6 一樣，只要在後面加一個 `=` 就搞定啦！

## 其餘參數

在 ES6 之後多了`...`運算子，那我們要如何在 TS 當中使用呢？

```
// 編譯前
function func1(name: string, ...nums: number[]) {
  console.log(name, nums)
}
func1('Cheeto', 1, 2, 3, 4, 5)

// 編譯後
function func1(name) {
    var nums = [];
    for (var _i = 1; _i < arguments.length; _i++) {
        nums[_i - 1] = arguments[_i];
    }
    console.log(name, nums);
}
func1('Cheeto', 1, 2, 3, 4, 5); // Cheeto [1, 2, 3, 4, 5]
```

在這邊有一個小重點必須牢記，**其餘參數是陣列，所以在型別定義時必須是陣列唷！**

## 函式型別也能使用聯合型別

```
// 編譯前
function reverse(item: number | string): number | string {
  if (typeof item === 'number') {
    return item.toString().split('').reverse().join('');
  } else {
    return item.split('').reverse().join('');
  }
}
reverse('Cheeto')

// 編譯後
function reverse(item) {
    if (typeof item === 'number') {
        return item.toString().split('').reverse().join('');
    }
    else {
        return item.split('').reverse().join('');
    }
}
reverse('Cheeto'); // 回傳 oteehC
```

又學到了一課 ^^~

## 型別斷言

當 TS 不能確定一個聯合型別的變數到底是哪個型別的時候，我們可以利用型別斷言告訴 TS。

<br>

```
function getLen(item: number | string): number {
  // TS 沒辦法分辨參數是 number 還是 string，所以不能確定能不能取到 length，導致報錯
  if (item.length) {
    return item.length
  } else {
    return item.toString.length;
  }
}

// 會報錯：Property 'length' does not exist on type 'number'.
```

像這種時候就可以透過**型別斷言**來告訴 TS，我可以確定這個是 `string`。

```
function getLen(item: number | string): number {
  if ((<string>item).length) {
    return (<string>item).length;
  } else {
    return item.toString.length;
  }
}
```

意思就是只有 `string` 的型別能取到 `length`，所以你可以透過型別斷言來告訴 TS 我確定這個是 `string`。