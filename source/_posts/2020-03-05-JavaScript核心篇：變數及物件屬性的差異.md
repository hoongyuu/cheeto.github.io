---
title: JavaScript核心篇：變數及物件屬性的差異
date: 2020-03-05 16:44:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 變數及物件屬性的差異

```
var a = 1;
b = 2;
console.log(window);
```

這邊執行 window 會發現 a、b 都在 window 裡面。

![變數與屬性差異](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E8%AE%8A%E6%95%B8%E8%88%87%E5%B1%AC%E6%80%A7%E5%B7%AE%E7%95%B0.jpg?alt=media&token=5425e25f-c9b8-4675-8a27-92259b5941bc)

但是這兩種語法是有差別的，a 在 window 裡面它是變數，但是 b 則是屬性。那這兩者的差別又在於「**變數無法被刪除，屬性可以**」。

```
var a = 1;
b = 2;

delete a;
delete b;

// 看看 a, b 是否還存在
console.log(a);
console.log(b);
```

![變數與屬性刪除](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E8%AE%8A%E6%95%B8%E8%88%87%E5%B1%AC%E6%80%A7%E5%88%AA%E9%99%A4.jpg?alt=media&token=6bcf1f53-2157-4ce0-8946-7bb570336628)

在下方也可以看到兩者的差異

![補充](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E8%A3%9C%E5%85%85%E8%AE%8A%E6%95%B8%E8%88%87%E5%B1%AC%E6%80%A7.jpg?alt=media&token=2be297aa-b743-4b6a-8c14-138eb1bfa3f3)