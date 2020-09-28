---
title: JavaScript：ES6 - ... 其餘及展開
date: 2020-08-27 16:08:34
tags:
  - JavaScript
categories: 
  - JavaScript
---

# JavaScript：ES6 - `...` 其餘及展開

## ES6： `...` 其餘及展開

**ES6** 多了一個 `...` 的其餘及展開的方法，而這個方法可以實作在許多的用途上面，那就讓我們來看看 `...` 的實作方法吧！

### 合併陣列的方式

過去我們要合併陣列時，都會使用 `concat` 的陣列方法，但是現在可以直接通過 `...` 展開來實踐。

```
let groupA = ['小明', '杰倫', '阿姨'];
let groupB = ['老媽', '老爸'];
let groupAll = [...groupA, ...groupB];
console.log(...groupA); // 回傳 小明 杰倫 阿姨
console.log(groupAll); // 回傳 ['小明', '杰倫', '阿姨', '老媽', '老爸']
```

這邊可以看到如果直接回傳 `...groupA` 它是會一個一個展開取出裡面的值。


### 利用 `...` 做到淺層複製

之前知道可以用 `Object.assign`，但是通過 `...` 展開之後，不管是**陣列**還是**物件**也是可以做到淺層複製，實在是方便且快速！

```
let groupA = ['小明', '杰倫', '阿姨'];
let groupB = [...groupA]; // 這裡 groupB 已經是一個新的陣列
groupB.push('阿明');
console.log(groupA); // 回傳 ['小明', '杰倫', '阿姨'];
```

```
const GinyuTeam = {
  Ginyu: {
    name: '基紐'
  },
  Jeice: {
    name: '吉斯'
  },
  burter: { 
    name: '巴特'
  },
};

const newTeam = { ...GinyuTeam };
console.log(newTeam);
```

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E6%B7%BA%E8%A4%87%E8%A3%BD.jpg?alt=media&token=59e9250a-27a6-4018-a04d-72ef260a128c)


### 類陣列處理

當遇到類陣列的時候，我們可以通過 `...` 展開將**類陣列**轉換成陣列。

```
function updateEasyCard() {
  const arg = [...arguments]; // arguments 本來是類陣列，把它轉換成陣列
  const sum = arg.reduce(function (a, b) {
    return a + b; 
  }, 0);
  console.log('我有 ' + sum + ' 元');
};
updateEasyCard(10, 50, 100, 50, 5, 1, 1, 1, 500); // 回傳 我有 718 元
```

`arguments`本來是一個類陣列，並不能使用 `reduce` 的方法，但是我們可以利用 `...` 來轉換成陣列。


### 其餘參數

本來在 **ES6** 之前，都是使用 `arguments` 來取得其餘參數，不過 `arguments` 是類陣列，所以很多陣列方法並不能用，都必須轉換成陣列，多了一個步驟。

現在 **ES6** 推出了 `...` 來取得其餘參數，可以直接設定名稱直接取得之外，它還是一個陣列，所以可以直接使用陣列方法。

```
function moreMoney(name, ...money) {
  console.log(name, money);
};
moreMoney('小辣椒', 100, 100, 100); // 小辣椒 [100, 100, 100]
```

這邊要特地說一個重點，利用其餘參數所回傳的會是一個真正的**陣列**。



