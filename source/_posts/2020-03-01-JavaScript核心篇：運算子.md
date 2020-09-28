---
title: JavaScript核心篇：運算子
date: 2020-03-01 18:50:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 運算子

運算子一定會回傳一個結果，JavaScript 常見的運算子有二元運算子、一元運算子，以及一種特殊的 三元運算子，也就是 條件運算子。

![運算子](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E9%81%8B%E7%AE%97%E5%AD%90.jpg?alt=media&token=774d5f5a-db3b-4b9b-9f7a-e715d5e7154d)

<!--more-->

二元運算子最常見的就是下面這種運算子

>運算元1 運算子 運算元2

## 一元運算子

一元運算子是只需要一個運算元的運算。

**delete**

delete 就算是一元運算子。可以用來刪除物件、物件的屬性，或者在陣列中選取索引指定刪除的目標。語法如下

```
delete 物件名稱;
delete 物件名稱.屬性;
delete 物件名稱[索引];
```

**typeof**

typeof 也算是一元運算子。

## 三元運算子

條件運算子 是 JavaScript 唯一的三元運算子。

```
//語法
(condition) ? 'truthy' : 'falsy';
```

如果條件成立它會回傳 'truthy' 裡面的值，否則回傳 'falsy'。

```
let bmi = 22
bmi < 20 ? '偏瘦' : '偏胖';
```

![三元運算判斷](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E4%B8%89%E5%85%83%E9%81%8B%E7%AE%97%E5%88%A4%E6%96%B7.jpg?alt=media&token=73886c5d-0e74-4fb0-b493-87d0cd1ef60d)