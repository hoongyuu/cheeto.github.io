---
title: JavaScript：ES6 - 解構賦值
date: 2020-09-03 19:31:20
tags:
  - JavaScript
categories: 
  - JavaScript
---

# JavaScript：ES6 - 解構賦值

**ES6** 解構賦值的方法就像鏡子一樣，能夠一一的設定變數去取得物件、陣列的元素。

## 從陣列中解構賦值

```
const people = ['小奇', '小念', '小淵', '小富', '小昱'];
const [chi, nian, yuan, fu, yu] = people;

console.log(chi, nian, yuan, fu, yu); // 小奇 小念 小淵 小富 小昱
```

甚至也能 ↓

```
const people = ['小奇', '小念', '小淵', '小富', '小昱'];
const [chi, nian, , , yu] = people;
console.log(chi, nian, yu); // 小奇 小念 小昱
```

如果在當中留下空格的話，也能直接略過對應的元素，因此可以彈性的設定自己需要的變數。

<!--more-->

## 從字串當中解構賦值

字串也是能夠解構賦值，如下 ↓

```
const name = 'Cheeto';
const [a, b, c, d, e, f] = name;

console.log(a, b, c, d, e, f); // C h e e t o
```

## 從物件當中解構賦值

```
const people = {
  chi: '小奇',
  nian: '小念',
  yuan: '小淵',
  fu: '小富',
};
const { chi, fu } = people;

console.log(chi, fu); // 小奇 小富
```

物件當中使用解構賦值的話能夠利用屬性名稱去取得，如果沒有設定變數名稱的話，預設名稱就是屬性名稱。

那就來試試看如何設定變數名稱吧 ↓

```
const people = {
  chi: '小奇',
  nian: '小念',
  yuan: '小淵',
  fu: '小富',
};
// { 取得的屬性名稱: 要賦予的變數名稱 }
const { chi: chichi, fu: fufu } = people;

console.log(chichi, fufu); // 小奇 小富
```

### 從物件當中解構賦值 - `...運算子`

```
const people = {
  chi: '小奇',
  nian: '小念',
  yuan: '小淵',
  fu: '小富',
};
const { chi: chichi, ...other } = people;

console.log(chichi, other); // 小奇 {nian: "小念", yuan: "小淵", fu: "小富"}
```

### 從物件當中解構賦值 - 參雜陣列

如果物件當中的屬性有陣列的話，我們能夠依序上面學到的方式組合起來使用。

```
const people = {
  chi: '小奇',
  nian: '小念',
  yuan: '小淵',
  fu: '小富',
  ary: ['小昱', '小花']
};
const { chi: chichi, ary:[, hua] } = people;

console.log(chichi, hua); // 小奇 小花
```


## 解構賦值 - 預設值

在解構賦值裡面設定預設值的話，如果沒有找到對應的元素，就會是預設值。

```
const [chi = '小奇'] = [];
console.log(chi); // 小奇
```

下列範例中可以看到如果找到對應的元素，就會是元素的值。

```
const [ chi = '奇奇', fu = '小富' ] = ['小奇'];
console.log(chi, fu); 小奇 小富
```

## 解構賦值 - forOf

```
const family = [
  {
    name: '小奇',
    family: {
      father: '奇爸爸',
      mother: '奇媽媽',
    },
  },
  {
    name: '小富',
    family: {
      father: '富爸爸',
      mother: '富媽媽',
    },
  },
];

for (const {name, family: { father: papa, mother: mama } } of family) {
  console.log(name, papa, mama);
};
// 小奇 奇爸爸 奇媽媽
// 小富 富爸爸 富媽媽
```