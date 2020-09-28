---
title: JavaScript：indexOf()
date: 2020-08-27 17:04:00
tags:
  - JavaScript
categories: 
  - JavaScript
---

# JavaScript：indexOf()

`indexOf()` **可以尋找你要找尋的"值"當中首次出現的位置**，若是找不到匹配的值會回傳 -1 的值，如果有找到則會回傳取得位置的值。

## 利用 `indexOf` 尋找元素

```
const name = ['小奇', '小念', '小淵', '小富'];

console.log(name.indexOf('小淵')); // 回傳 2，因為是在索引位置 2 找到
console.log(name.indexOf('小昱')); // 回傳 -1，
```

<!--more-->

## 搭配 `map` 在物件當中尋找元素索引位置

這是利用 `map` 把物件的屬性逐筆取出來組成陣列，再利用 `indexOf` 來取得索引位置的技巧。

```
const ary = [
  {
    name: '小奇',
    city: '高雄市'
  },
  {
    name: '小念',
    city: '台北市'
  },
  {
    name: '小淵',
    city: '台中市'
  },
  {
    name: '小富',
    city: '台南市'
  }
];

console.log(ary.map(item => item.name).indexOf('小淵')); // 回傳 2

分解如下 ↓

const newAry = ary.map(item => item.name);
console.log(newAry) // 回傳 ["小奇", "小念", "小淵", "小富"]
console.log(newAry.indexOf('小淵')); // 回傳 2
```

透過 `map` 回傳所有 name 的值並組成陣列，再利用 `indexOf` 來取得指定的元素的索引值。

`map` 方法還有一個好處，就算陣列當中其中有一個物件沒有 `name` 的屬性，也會回傳一個 `undefined`，所以取到的值基本上就會是正確的索引值！

## `indexOf` 過濾重複的值

```
const ary = [
  {
    name: '小奇',
    city: '高雄市'
  },
  {
    name: '小念',
    city: '台北市'
  },
  {
    name: '小淵',
    city: '台中市'
  },
  {
    name: '小富',
    city: '台南市'
  },
  {
    name: '小昱',
    city: '高雄市'
  }
];

const filterCity = [];

ary.forEach(item => {
  if (filterCity.indexOf(item.city) === -1) {
    filterCity.push(item.city);
  };
});

console.log(filterCity);  // 回傳 ["高雄市", "台北市", "台中市", "台南市"]
```

在 `ary` 的陣列當中可以看到高雄市出現兩次，那如果要把程式篩選出來可以透過 `indexOf` 做到。


## indexOf() 尋找關鍵字

`indexOf` 可以用來尋找關鍵字，也可以利用這個方法來做到過濾的效果。

```
const ary = [
  {
    name: '小奇',
    city: '高雄市'
  },
  {
    name: '小念',
    city: '台北市'
  },
  {
    name: '小淵',
    city: '台中市'
  },
  {
    name: '小富',
    city: '台南市'
  },
  {
    name: '小昱',
    city: '高雄市'
  }
];

ary.forEach(item => {
  if (item.city.indexOf('高雄市') !== -1) {
    console.log(item); 
  };
});
```

回傳如下 ↓

```
{name: "小奇", city: "高雄市"}
{name: "小昱", city: "高雄市"}
```