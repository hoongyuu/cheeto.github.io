---
title: JavaScript：陣列方法
date: 2020-08-27 15:47:34
tags:
  - JavaScript
categories: 
  - JavaScript
---

# JavaScript：陣列方法

這篇文章介紹的是陣列的方法，一共會介紹下列幾種：

* forEach
* map
* filter
* find
* every
* some
* reduce
* fill
* sort
* concat
* Array.from

<!--more-->

以下面的陣列為例子 ↓

```
const people = [
  {
    name: '小明',
    money: 500
  },
  {
    name: '漂亮阿姨',
    money: 3000
  },
  {
    name: '杰倫',
    money: 60000
  },
  {
    name: '老媽',
    money: Infinity
  }
];
```

## forEach

`forEach` 可以設定三個參數，分別是：本身的值、物件索引、陣列本身

```
people.forEach((item, index, array) => {
  item.icash = item.money + 500;
  return item.icash;
})

console.log(people);
```

回傳結果：

```
0: Object { name: "小明", money: 500, icash: 1000 }
1: Object { name: "漂亮阿姨", money: 3000, icash: 3500 }
2: Object { name: "杰倫", money: 60000, icash: 60500 }
3: Object { name: "老媽", money: Infinity, icash: Infinity }
```

可以看到每個物件都加上了 `icash` 的屬性。


## map

`map` 跟 `forEach` 很像，但是它需要回傳一個值，而它會透過回傳的值組成陣列。

```
const newPeople = people.map((item, index) => {
  item.icash = item.money + 500;
  return item.icash;
})

console.log(newPeople); // 回傳 [ 1000, 3500, 60500, Infinity ]
```

但是如果透過篩選的方式就不太適合 `map` 了

```
const newPeople = people.map((item, index) => {
  if (item.money === 60000) {
    return item
  }
})

console.log(newPeople) // [ undefined, undefined, 60000, undefined ]
```

使用 `map` 的話不管怎樣它就是會回傳根本來陣列數一樣的長度，而多餘的就回傳 `undefined`。

## filter

`filter` 顧名思義就很適合拿來做篩選了，它能夠透過判斷把要回傳的值回傳並組成陣列。

```
const newPeople = people.filter((item, index) => {
  if (item.money < 5000) {
    // 只能回傳 true 或 false
    // 如果輸入 return item.money 也只會回傳物件
    return true
  }
})

console.log(newPeople)
```

結果如下 ↓

```
0: Object { name: "小明", money: 500 }
1: Object { name: "漂亮阿姨", money: 3000 }
```

這邊就可以看到 `filter` 跟 `map` 的差別了，`filter` 只會回傳篩選過後的值，並不會像 `map` 還會帶入 `undefined`。

## find

`find` 會透過判斷找出第一個符合條件的值，並把它回傳。

```
const newPeople = people.find((item, index) => {
  if (item.money < 5000) {
    return item
  }
})

console.log(newPeople) // { name: "小明", money: 500}
```

這邊就能看到 `find` 跟 `filter` 的差別了，一樣的判斷式，但是 `find` 只會回傳它判斷為 `true` 的第一筆數據。

## every

`every` 是用來篩選所有的值的方法，就有點像是判斷式裡面的 `&&`，只要其中一個條件是 `false` 它就會回傳 `false`。

```
let newPeople = people.every((item, index) => {
  if (item.money > 300) {
    return true
  }
})

console.log(newPeople) // true

newPeople = people.every((item, index) => {
  if (item.money > 1000) {
    return true
  }
})

console.log(newPeople) // false
```

## some

`some` 是用來篩選所有的值的方法，就有點像是判斷式裡面的 `||`，只要其中一個條件是 `true` 它就會回傳 `true`。

```
const newPeople = people.some((item, index) => {
  if (item.money < 5000) {
    return true
  }
})

console.log(newPeople) // true
```

這邊即使 **杰倫、老媽** 的錢大於 **5000**，它還是會回傳 `true`，只要其中有一筆資料是回傳`true`，它就會回傳 `true`。

## reduce

`reduce` 就跟前面有所差異，它是能夠跟前一個回傳的值加總的方法，常常用來做加總的動作。

```
const money = [500, 1000, 1500, 2000]

// 三個參數分別為： 前一個回傳值、本身的值、本身的索引。
// 後面 0 這個參數是起始值，如果設定 100 就會從 100 開始加。
const moneyAll = money.reduce((prev, item, index) => {
  console.log(prev); // 回傳五個值分別為：0,500,1500,3000,5000
  return prev + item
}, 0)

console.log(moneyAll) // 5000
```

`reduce` 也能夠透過比較的方式來做篩選，像是把篩選出最大的值。

```
const money = [500, 2000, 1500, 600]

const moneyAll = money.reduce((prev, item, index) => {
  console.log(prev)
  return Math.max(prev, item)
}, 0)

console.log('moneyAll',moneyAll)
```

回傳如下 ↓

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2FreduceConsole.jpg?alt=media&token=aa06836f-34d3-4b8b-a426-9460f9b34ffc)

它會一個一個比較最後取出最大的金額回傳。

## fill

`fill` 能夠將陣列的元素轉換成指定的**值**，第一個參數是指定要置換的值、第二個是起始位置、第三個是結束置換位置往後一個值。

```
const newPeople = {
  name: '爺爺',
  money: 8800
};

// fill('指定要轉換的值')
console.log(people.fill(newPeople));
```

回傳如下 ↓

```
0: {name: "爺爺", money: 8800}
1: {name: "爺爺", money: 8800}
2: {name: "爺爺", money: 8800}
3: {name: "爺爺", money: 8800}
```

### 也能將值置換特定的位置

```
const newPeople = {
  name: '爺爺',
  money: 8800
};

// fill('指定要轉換的值', '從哪個位置開始', '結束置換的後一個位置')
console.log(people.fill(newPeople, 1, 3));
```

回傳如下 ↓

```
0: {name: "小明", money: 50}
1: {name: "爺爺", money: 8800}
2: {name: "爺爺", money: 8800}
3: {name: "老媽", money: Infinity}
```

## sort

`sort` 能夠用來進行排序的動作，能夠將陣列內的元素以大到小、小到大的順序進行排序。

```
people.sort((a, b) => b.money - a.money);
console.log(people);
```

回傳如下 ↓

```
0: {name: "老媽", money: Infinity}
1: {name: "杰倫", money: 60000}
2: {name: "漂亮阿姨", money: 3000}
3: {name: "小明", money: 50}
```

## concat 

`concat` 可以將陣列合併在一起，不過在 ES6 當中已經可以用 `...展開` 來替代。

```
const newPeople = [
  {
    name: '爺爺',
    money: 8800
  },
  {
    name: '奶奶',
    money: 9999
  }
];

const family = people.concat(newPeople);
const family1 = [...people, ...newPeople];
console.log(family);
console.log(family1)
```

回傳如下 ↓

```
0: {name: "小明", money: 500}
1: {name: "漂亮阿姨", money: 3000}
2: {name: "杰倫", money: 60000}
3: {name: "老媽", money: Infinity}
4: {name: "爺爺", money: 8800}
5: {name: "奶奶", money: 9999}

0: {name: "小明", money: 500}
1: {name: "漂亮阿姨", money: 3000}
2: {name: "杰倫", money: 60000}
3: {name: "老媽", money: Infinity}
4: {name: "爺爺", money: 8800}
5: {name: "奶奶", money: 9999}
```

可以看到用 `concat` or `...展開` 都可以得到相同的結果。

## Array.from

`Array.from` 跟 `map` 很像，但是它能夠通過回傳讓**類陣列**、**可迭代物件**轉換成陣列。它可以設定兩個參數，第一個參數是指定的陣列、類陣列、可迭代物件、第二個則是改變陣列元素的函式。

```
const doubleMoney = Array.from(people, item => {
  return item.money + item.money;
});
console.log(doubleMoney);
```

回傳 ↓

```
0: 1000
1: 6000
2: 120000
3: Infinity
```

這邊有一個類陣列，可以利用 `Array.from` 把它轉換成陣列。

```
const aryLike = {
  0: '小明', 
  1: '漂亮阿姨',
  2: '杰倫',
  3: '老媽',
  length: 4
};
const ary = Array.from(aryLike)
console.log(ary);
```

回傳如下 ↓

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%E7%AD%86%E8%A8%98%2Farray-console.jpg?alt=media&token=c0477916-c723-462d-a116-6ceafac9cb3e)