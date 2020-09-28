---
title: CSS：overflow 搭配 CSS 做出滑動效果
date: 2020-01-20 13:07:21
tags:
  - css
categories: 
  - css
---

# overflow搭配CSS做出滑動效果

<br/>

[codePen 範例參考](https://codepen.io/Chee7o/pen/BayGQVy)

HTML環境設置：

``` 
  <div class="box">
    <h1 class="title">商品標題</h1>
  </div>
```

<br/>

這個效果是讓滑鼠hover到box的時候，讓title滑動出來的 transition 特效。

CSS如下

``` 
.box {
      position: relative;
      margin: 0 auto;
      width: 350px;
      height: 200px;
      border: 2px solid #ccc;
      overflow: hidden;
    }

    .box:hover .title {
      left: 0;
    }

    .title {
      position: absolute;
      left: -45px;
      height: 100%;
      background-color: brown;
      color: rgb(233, 233, 233);
      padding: 0 12px;
      -webkit-writing-mode: vertical-lr;
      writing-mode: vertical-lr;
      text-align: center;
      font-weight: bold;
      letter-spacing: 2px;
      transition: all 1.5s;
    }
```

這段程式碼是利用**絕對定位**把.title轉移到.box之外的位置，再利用**overflow**可以隱藏超出區塊外內容的特性，先把.title區塊隱藏到.box之外，然後利用hover讓滑鼠滑到.box的時候.title會出現。

接著利用transition讓他產生動畫，這樣就能產生滑動的效果了！

