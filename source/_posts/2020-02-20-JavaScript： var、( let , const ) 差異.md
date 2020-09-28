---
title: 'JavaScript： var、( let , const ) 差異'
date: 2020-02-20 16:44:11
tags:
  - JavaScript
categories: 
  - JavaScript
---

# JavaScript： var、( let , const ) 差異



## 前言

在ES6之前，JavaScript要宣告變數的時候，會使用到 var 宣告變數，
但是到了ES6之後，建議盡量都用 ( let , const ) 來做宣告，不要再用 var 了。

因為 var 有一個缺點，那就是它很容易汙染到全域變數。 如下

```
    var a = 15;
    
    console.log(a);  // 15
    //用 var 的話會讓 a 直接跑到 window 下面變成全域變數
    console.log(window.a);  // 15
```


## var、( let , const ) 差異在哪？

我們開發時應該盡量避免汙染到全域變數，所以ES6因為這個原因發明了 「let」、「const」，來改善這個問題，那它們之間的差異在哪裡呢？ 讓我們繼續看下去。


### let / const 是以 **`{}`** 來做區隔的，而 var 是以 function 來做區隔。

```
    for (var i = 0; i < 3; i++) {
      console.log(i)
    }    //  0 / 1 / 2 三個值沒有問題，但是重點來了！
    
    console.log(i) // 3
```

發現問題點了嗎？ 在for迴圈裏面用 var 宣告的 i (變數) 已經污染到全域變數了！

遇到這樣的問題的話，let 其實就很好解決了，因為 let 是用 **`{}`** 來做區隔的，所以它並不會汙染到全域變數。 如下

```
    for (let i = 0; i < 3; i++) {
      console.log(i)
    }    //  0 / 1 / 2
    
    console.log(i) // Uncaught ReferenceError: i is not defined
```

如果用 let 宣告的話會出現 i is not defined 這樣的結果。

<br>


### let / const 沒有變數提升的這個特性，var 有變數提升的特性。

```
    console.log(a); // Cannot access 'c' before initialization
    let a = 15;
    console.log(a); // 15 
    
    
    console.log(b); // undefined
    var b = 15;
    console.log(b); // 15
```

使用 let 宣告的話並不會有變數提升的特性，所以在宣告之前它並不能讀取出來。

相反的是 var 可以，因為 var 有變數提升的特性所以它其實是變成這樣。 如下

```
    var b;
    console.log(b); // undefined
    var b = 15;
    console.log(b); // 15
```

變數提升的特性會讓 b 宣告出現在最上方，但是它的「值」會在原地立正站好，並沒有那麼的聽話呀！！

<br>

### let / const 不能再同一個區塊重複命名！！！

var 在同一個區塊上重複宣告也沒有關係，但是 let / const 是沒有辦法的。 如下

```
    var a = 5;
    var a = 10;
    console.log(a); // 10
    
    let b = 5;
    let b = 10; // Identifier 'c' has already been declared
```

在用 let 再一次宣告的時候，會先跳出 'c' has already been declared 這樣的錯誤，理所當然就沒辦法 console 了。



---


最後要建議所有人：不管是 var 或者 let / const，在使用變數前都要先宣告，養成良好的 coding 習慣才是第一關鍵！
