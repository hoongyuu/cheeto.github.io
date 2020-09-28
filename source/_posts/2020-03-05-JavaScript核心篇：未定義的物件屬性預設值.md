---
title: JavaScript核心篇：未定義的物件屬性預設值
date: 2020-03-05 20:03:40
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 未定義的物件屬性預設值

在 JavaScript 的物件下，如果去查找該物件不存在的屬性，它不會回傳 not defined，而是會回傳 undefined。

```
var family = {
    name: '小明家'
};
console.log(family.ming); // undefined
```

這邊如果這樣做

```
var family = {
    name: '小明家'
};
console.log(family.ming); // undefined
family.ming.name = '小明';
```

這邊會回傳這樣 ↓

![未定義物件屬性](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E6%9C%AA%E5%AE%9A%E7%BE%A9%E7%89%A9%E4%BB%B6%E5%B1%AC%E6%80%A7.jpg?alt=media&token=83f55d92-3526-4f69-94fb-82505d0717ee)

它會跳錯是因為你不能對一個未定義的屬性再增加一個屬性進去。

如果我們想要解決這個問題可以這樣

```
var family = {
    name: '小明家',
    ming: {}
};
family.ming.name = '小明';
console.log(family);
```

或

```
var family = {
    name: '小明家'
};
family.ming = {
    name: '小明'
};
console.log(family);
```

結果都會如下 ↓

![未定義物件解決](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E6%9C%AA%E5%AE%9A%E7%BE%A9%E7%89%A9%E4%BB%B6%E8%A7%A3%E6%B1%BA%E6%96%B9%E6%B3%95.jpg?alt=media&token=f719539f-fac1-4ce2-8936-20665d88f229)

<br>

如果我們對 name 進行設定的話呢？

```
var family = {
    name: '小明家'
};
family.name.my = '小明';
console.log(family.name); // 小明家
```

這邊為什麼不能加呢？因為純值無法新增屬性！！！詳情請點[這裡](https://hoongyuu.github.io/cheeto.github.io/2020/03/05/2020-03-05-JavaScript%E6%A0%B8%E5%BF%83%E7%AF%87%EF%BC%9A%E7%89%A9%E4%BB%B6%E8%88%87%E7%B4%94%E5%80%BC)


