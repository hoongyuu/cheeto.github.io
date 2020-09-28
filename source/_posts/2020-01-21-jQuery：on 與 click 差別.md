---
title: jQuery：on與click的差別
date: 2020-01-21 15:44:51
tags:
  - jQuery
categories: 
  - jQuery
---

# on與click的差別

<br/>

在jQuery當中，時常會使用到 on、click 這兩種方式來操控你要的DOM，那兩者差別在哪？


## click

click只會對現在html裡面你指定的元素有效。

假設html環境如下


```
  <div class="wrap">
    <div class="box1">
    </div>
    <div class="box2">
      <input type="button" value="通知" class="alertBtn">
    </div>
  </div>
```

js環境如下

```
$('.alertBtn').click(function (e) { 
  e.preventDefault();
  alert('通知出現')
});

$('.box1').html('<input type="button" value="jQuery通知" class="alertBtn">');
```

以這個假設的環境來說的話，因為click的事件是在.box1新增button之前所設定，所以如果點擊 <font color=#CCCCFF>**jQuery通知**</font> 這個按鈕就不會執行alert。
但是如果把 <font color=#CCCCFF>**jQuery通知**</font> 放到click事件之前 (如下)，那 <font color=#CCCCFF>**jQuery通知**</font> 就能夠執行alert。

```
$('.box1').html('<input type="button" value="jQuery通知" class="alertBtn">');

$('.alertBtn').click(function (e) { 
  e.preventDefault();
  alert('通知出現')
});
```

<br/>

## on

<br/>

on就像是監聽，他可以隨時監控你的行為，就算是後來才用jQuery、JS新增的標籤它都會隨時保持關注。

所以你不管是

```
  $('.wrap').on('click', '.alertBtn', function () {
    alert('通知出現')
  });

  $('.box1').html('<input type="button" value="jQuery通知" class="alertBtn">');
```

或者是

```
  $('.box1').html('<input type="button" value="jQuery通知" class="alertBtn">');

  $('.wrap').on('click', '.alertBtn', function () {
    alert('通知出現')
  });
```

順序不管是怎麼放它都有辦法監聽到，而且on所佔的記憶體還比click還少唷！