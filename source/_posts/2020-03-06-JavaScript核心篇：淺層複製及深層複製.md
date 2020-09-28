---
title: JavaScript核心篇：淺層複製及深層複製
date: 2020-03-06 18:33:22
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 淺層複製及深層複製

## 淺層複製 (Shallow Copy)

```
var family = {
    name: '小明家',
    members: {
      dad: '老爸',
      mom: '老媽',
      ming: '小明'
    }
};
var newFamily = {};
for (var key in family){
  console.log(key)
}
```

![淺拷貝](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E6%B7%BA%E6%8B%B7%E8%B2%9D.jpg?alt=media&token=30901fad-8369-4e1c-8cfd-e2af59d82567)

這裡可以看到 `key` 的值其實就是 `family` 的第一層屬性。

所以我們可以利用這種方式做到第一層的複製。 如下 ↓

```
var family = {
    name: '小明家',
    members: {
      dad: '老爸',
      mom: '老媽',
      ming: '小明'
    }
};
var newFamily = {};
for (var key in family){
  newFamily[key] = family[key];
}
console.log(newFamily);
```

這樣就可以利用 `key`  依序把第一層的屬性 `name`,`members` 取出來放到 `newFamily` 裡面。

![淺拷貝2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E6%B7%BA%E6%8B%B7%E8%B2%9D2.jpg?alt=media&token=9906bd33-c66b-4eb4-997d-f5ffc1abe901)

這裡 `family` 跟 `newFamily` 就不會是在同一個位址上，我們可以換一種方式來測試。

```
var family = {
    name: '小明家',
    members: {
      dad: '老爸',
      mom: '老媽',
      ming: '小明'
    }
};
var newFamily = {};
for (var key in family){
  newFamily[key] = family[key];
}

newFamily.name = '杰倫家';
console.log(family);
console.log(newFamily);
```

會出現下面這樣的結果 ↓

![淺拷貝3](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E6%B7%BA%E6%8B%B7%E8%B2%9D3.jpg?alt=media&token=194a33ef-e39b-4f5c-9c8d-83f468438c92)

由此可知它們已經完全沒有關係了。((但是只限第一層喔！

原因是為什麼呢？ 我們接著看下去 ↓

```
var family = {
    name: '小明家',
    members: {
      dad: '老爸',
      mom: '老媽',
      ming: '小明'
    }
};
var newFamily = {};
for (var key in family){
  newFamily[key] = family[key];
}

newFamily.name = '杰倫家';
newFamily.members.ming = '杰倫';
console.log(family);
console.log(newFamily);
```

結果如下 ↓

![淺拷貝4](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E6%B7%BA%E6%8B%B7%E8%B2%9D4.jpg?alt=media&token=55bbec2d-e57b-443e-b6db-50cc15996892)

原因是 `newFamily` 宣告了新物件也把 `family` 第一層的屬性依序加進去，但是 `members` 本來就是一個物件了！所以你把 `members` 丟到 `newFamily` 其實也是把一個參考位址丟過去。(在 '取值&取址'章節 有講到)

這種方式就叫做「淺層複製」也能稱為「淺拷貝」。

上面講的是基本原理，現在除了 `for in` 之外也有其他方法可以很快速的做出這樣的淺層複製，讓我們繼續看下去。

第一種是利用 jQuery 的方式，語法如下 ↓

```
var newFamily = jQuery.extend({}, family);
```

第二種是新的 ES6 才有的語法 ↓

```
var newFamily = Object.assign({}, family);
```

上述的兩種方法都能夠做到淺層複製的效果喔！

## 深層複製 (deep copy)

```
var family = {
    name: '小明家',
    members: {
      dad: '老爸',
      mom: '老媽',
      ming: '小明'
    }
};

// 深層複製語法 ↓
var newFamily = JSON.parse(JSON.stringify(family));

newFamily.name = '杰倫家';
newFamily.members.ming = '杰倫';
console.log(family)
console.log(newFamily);
console.log(family === newFamily);
```

原理是把 `family` 裡面的所有東西轉成字串之後，本身的記憶體參考位址會消失，然後再轉回物件的時候，又會再指向新的一個記憶體參考位址。

所以利用著這個方式就可以做到「深層複製」也能稱為「深拷貝」。