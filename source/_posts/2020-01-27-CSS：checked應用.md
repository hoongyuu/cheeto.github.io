---
title: CSS：checked 互動技巧
date: 2020-01-27 17:35:15
tags:
  - css
categories: 
  - css
---

# CSS：checked 互動技巧

CSS的:checked 表單狀態選取器，這個選取器是能夠選取 checkbox 被勾選的狀態，而這個技巧能夠幫助我們在不需要用到程式的情況之下，也能夠在網頁上做到互動的效果唷！

下面就讓我們試試看吧！！

[Demo](https://codepen.io/Chee7o/pen/zYGwrQG)

首先我們可以先做出像這樣的圖片

![初始照片](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/CSS%EF%BC%9Achecked%2Fcheck%E5%88%9D%E5%A7%8B.jpg?alt=media&token=ff6fd95a-3b7b-4f22-aec0-d5e4f5a6f6e0)

在這個照片當中我希望能夠點擊下面的icon時，下面的選單能夠收合。

![unchecked](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/CSS%EF%BC%9Achecked%2Funchecked.jpg?alt=media&token=5448e757-9c4c-483e-bf7d-c939c70ece0d)

我們能夠加入一個 checkbox ， 利用 label 把 icon 裝進去，再利用 label 去指向上面的 checkbox 來達到我們的互動效果！ 如下

```
#agent-callMe-switch:checked ~ .agent-callMe {
    margin-bottom: -111px;
}
```

上方程式碼的意思是：當 `#agent-callMe-switch` 被選取時，`.agent-callMe` 應該有什麼樣的樣式。

選取完之後就會像下方這樣

![checked](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/CSS%EF%BC%9Achecked%2Fchecked.jpg?alt=media&token=9ed59946-5837-41f2-bb24-e423cc58585c)

它選取時就能夠利用 `margin-bottom: -111px;` 把下方收起來，這裡就利用到了 checked 來做到了平常要利用程式才能做到的互動效果，太方便囉！

但是這樣還沒有做完呢！因為上面的 checkbox 還在，這樣根本不算一個能看的畫面！接下來我們就是要把 checked 隱藏起來。 如下

```
#agent-callMe-switch {
    position: absolute;
    opacity: 0;
    z-index: -1;
}
```

首先利用絕對定位讓 checkbox 不占空間，然後利用 `opacity` 讓它完全透明化，接著我們能夠利用 `z-index` 的效果確保我們不會點到它，因為 `opacity` 的效果只能夠讓它完全的透明，但其實還能夠點的到。

```
#agent-callMe-switch {
    position: absolute;
    visibility: hidden;
}
```
 
也能夠利用 `visibility: hidden;` 來做到這個效果，這個效果跟 `opacity` 的差別就是能不能被點到，利用 `visibility` 就不用再另為加上 `z-index`。

結果就會像這樣 ↓

![finish](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/CSS%EF%BC%9Achecked%2F%E9%9A%B1%E8%97%8Fcheck%E5%AE%8C%E7%95%A2.jpg?alt=media&token=d7e80bf9-f875-46e7-8fa8-7e5213c042d3)


文章就到這邊完畢啦！感謝