---
title: JavaScript核心篇：參數
date: 2020-03-09 14:28:12
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 參數


```
function callName(a){
    console.log('第一個：' +a);
    
    var a;
    console.log('第二個：' +a);
    a = '杰倫';
    console.log('第三個：' +a);
};
callName('小明');
```

會呈現 ↓

![參數覆蓋觀念](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8F%83%E6%95%B8%E8%A6%86%E8%93%8B%E8%A7%80%E5%BF%B5.jpg?alt=media&token=8d4db6c2-8da5-4e21-b1d8-d4875d8366f4)

所以說用宣告的方式其實沒辦法覆蓋掉的，如果想要覆蓋掉就直接定義一個新的值給 `a`。

<br>

下面還有另一個例子

```
function callName(a){
    console.log('第一個：' +a);
    
    function a(){};    
    var a;
    console.log('第二個：' +a);
    a = '杰倫';
    console.log('第三個：' +a);
};
callName('小明');
```

會呈現 ↓

![參數覆蓋觀念2](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8F%83%E6%95%B8%E8%A6%86%E8%93%8B%E8%A7%80%E5%BF%B52.jpg?alt=media&token=f424c988-01dd-435e-aae0-afb2ca1cfb34)

原因是因為函式會提升，但是本來定義的小明這個值是在函式的參數上面，而`function a`是在程式碼片段創造的，所以`function a`是會把小明這個值覆蓋掉的。


## 物件參數

```
function callObject(obj) {
    obj.name = '杰倫家';
};
var family = {
    name: '小明家'
};
callObject(family);
console.log(family); // 杰倫家
```

在函式參數當中如果是物件的話，還是會維持原本傳址的特性，所以 `family` 才會跟著被變動了。


## callback function

```
function functionB(fn) {
    fn('小明');
}
functionB(function (a) {
    console.log(a); // 小明
});
```

![callBackFunction](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2FcallBackFunction.jpg?alt=media&token=534e988b-1b4a-4e8f-8b47-123536002eb0)

* 洋紅色: functionB 執行時將函式作為參數傳入 fn，並在 functionB 內執行
* 綠色: fn 的小明作為參數傳遞給 functionB 執行時的函式

<br>

這邊換一個範例

```
function callSomeone(name, a) {
    console.log(name + '你好' + a);
};
function functionB(fn) {
    fn('小明', 1);
};
functionB(callSomeone); // 小明你好 1 
```


## Arguments

```
function callArg(a){
    console.log(a, argument)
};
callArg(1, 2, 3, '4')
```

回傳呈現 ↓

![Arguments](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2Farguments.jpg?alt=media&token=0622aef4-32c2-44c8-923b-9da533b71983)

arguments 是一個類陣列，它可以拿來做 for 迴圈，但是不能拿來做 `forEach` 之類的功能。