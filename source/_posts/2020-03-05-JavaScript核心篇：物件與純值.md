---
title: JavaScript核心篇：物件與純值
date: 2020-03-05 15:44:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 物件與純值

在 JavaScript 當中，純值是無法新增屬性的，只有物件型別可以新增屬性。

```
var newString = '小明家';
newString.name = '小明';
console.log(newString) // 小明家
```

因純值無法新增屬性，所以 newString 還是會維持本來的字串，不會做任何的修改。

<br>

現在我們來看第二個範例

```
var newString = new String('小明家');
newString.name = '小明家';

console.log(newString)
```

會顯示如下 ↓

![包裹物件範例](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8C%85%E8%A3%B9%E7%89%A9%E4%BB%B6%E7%AF%84%E4%BE%8B.jpg?alt=media&token=c3b2b553-4def-4fb7-83ea-009261022054)


因為包裹物件本來就會讓值轉為物件，所以 newString 自然就變為物件型別了，物件型別當然就能夠新增屬性啦！


<br>

再來我們看到陣列的範例

```
var newArray = [1, 2, 3];
newArray.name = '小明';
console.log(newArray);
console.log('typeof newArray: ' + typeof newArray);
```

會顯示如下 ↓

![陣列型別](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E9%99%A3%E5%88%97%E5%9E%8B%E5%88%A5.jpg?alt=media&token=ba15237d-5400-473c-b0bc-362ecc3ac601)

這樣應該就很清楚為什麼陣列可以新增屬性了吧！

<br>

最後讓我們看看 function(函式) 的範例

```
function callName() {
    console.log('呼叫小明');
}
console.log(typeof callName); // function
```

這邊在 typeof 會出現 function 是因為函式其實算是物件型別下的一個子型別，所以 function 算是物件型別。

接下來我們設定屬性看看 ↓

```
function callName() {
    console.log('呼叫小明');
}
callName.name = '小明';
console.dir(callName)
```

> `console.dir` 是能夠在 console 裡面展開函式的一個作法。

![函式型別範例1](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%87%BD%E5%BC%8F%E5%9E%8B%E5%88%A5%E7%AF%84%E4%BE%8B1.jpg?alt=media&token=44691349-7261-4226-9c14-d7717acb91d1)

這邊會發現為什麼 `callName.name = '小明';` 沒有作用，因為函式本身的 name 是無法被修改的，這邊的 name 其實就是函式本身的名稱。

```
function callName() {
    console.log('呼叫小明');
}
callName.ming = '小明';
console.dir(callName)
```

所以如果不是設定 name 為屬性的話，就可以順利的新增一個屬性了。 如下 ↓

![函式型別範例2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%87%BD%E5%BC%8F%E5%9E%8B%E5%88%A5%E7%AF%84%E4%BE%8B2.jpg?alt=media&token=4475ebc9-2171-4bf5-bd58-c30cf8476146)