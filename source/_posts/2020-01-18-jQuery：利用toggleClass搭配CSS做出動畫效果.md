---
title: jQuery：利用 toggleClass 搭配 CSS 做出動畫效果
date: 2020-01-18 15:44:01
tags:
  - jQuery
  - css
categories: 
  - jQuery
---

# 利用toggleClass搭配CSS做效果優化網站效能！

<br/>

jQuery雖然本來就可以直接用fadeToggle、slideToggle等.. 做效果，但是這樣的形式沒辦法讓網頁效能保持得很好，這時候就可以試試看用jQuery的toggleClass搭配CSS做一些效果吧！


<br/>

## toggleClass 開關效果

<br/>

[codePen 範例參考](https://codepen.io/Chee7o/pen/rNaQWbJ)

<br/>

toggleClass是可以在class裡面增加、刪除一個class，如果裡面有這個class就會刪除，反之增加。
<br/>

Html、CSS 程式碼範例：

``` 
<input type="button" value="開關" class="btn">

  <div class="text">
    內容...
  </div>
```

CSS如下

```
.btn{
  width: 60px;
  height: 40px;
  border: 2px solid #ccc;
}
.text{
  display: none;
  width: 500px;
}
.text.active{
  display: block;
}
```

在上方這段程式碼我有一個開關的按鈕，還有一個.text的區塊，假如一開始我預設.text是 display: none 的狀態下，要如何利用jQuery搭配CSS來開啟他呢？

<br/>

那就可以利用jQuery的toggleClass功能。

(如下)

```
$(document).ready(function () {
  $('.btn').click(function (e) { 
    e.preventDefault();
    $('.text').toggleClass('active');
  });
});
```

這段程式碼意思是按下btn的時候會執行toggleClass的動作，所以利用CSS選擇器的權重在.text裡面再新增一個.active的class就會把本來display:none變成display:block，這樣就能夠達到開關的效果了！

> [CSS權重觀念參考文章](https://ithelp.ithome.com.tw/articles/10196454) 

<BR/>

## 淡進淡出

<BR/>

[codePen 淡進淡出參考](https://codepen.io/Chee7o/pen/Jjoebwa)

<BR/>

淡進淡出是 toggleClass 開關效果的延伸利用，但是用CSS淡進淡出卻沒辦法讓區塊消失。
所以會把display:none/block刪除，因為把display留著沒辦法做出transition的動畫效果，之後新增opacity屬性，再利用transition動畫化！


只有CSS有差異。如下

```
.btn{
  width: 60px;
  height: 40px;
  border: 2px solid #ccc;
}
.text{
  width: 500px;
  opacity: 0;
  transition: all .5s;
}
.text.active{
  opacity: 1;
}
```

<br/>

## slide效果

<BR/>

[codePen slide參考](https://codepen.io/Chee7o/pen/XWJypmB)

<BR/>

slide效果是把整個區塊的height調整到0，然後利用overflow:hidden把區塊裡面的內容都隱藏起來，接著利用toggleClass把.active加入到.text裡面，讓整個區塊的高度回復，接著利用transition讓整個流程動畫化。

只有CSS有差異。如下

```
.btn{
  width: 60px;
  height: 40px;
  border: 2px solid #ccc;
}
.text{
  width: 500px;
  height: 0;
  transition: all .5s;
  overflow: hidden;
}
.text.active{
  height: 100px;
}
```
