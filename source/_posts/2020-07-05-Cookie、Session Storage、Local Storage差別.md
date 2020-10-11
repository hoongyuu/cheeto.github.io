---
title: Cookie、Session Storage、Local Storage差別
date: 2020-07-05 22:38:34
tags:
  - JavaScript
categories: 
  - JavaScript
---

# Cookie、Session Storage、Local Storage差別


## Cookie ─ 識別用戶

An HTTP cookie (web cookie, browser cookie) is a small piece of data that a server sends to the user’s web browser. The browser may store it and send it back with the next request to the same server.

Cookie 是伺服器傳送到使用者瀏覽器的一個"小"資料空間，瀏覽器可以透過 Cookie 儲存，在下次請求時回傳。

> [MDN](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies

<!--more-->

HTTP 是一種無狀態協定，意思是伺服器不會保存任兩個請求間的任何資料。伺服器藉由 Cookie 來讓同一個用戶的各項操作產生連結。

![](https://docs.microsoft.com/zh-tw/aspnet/web-api/overview/advanced/http-cookies/_static/image1.png)

> 取自網路

就像上圖所示，第一次發出請求時並沒有 Cookie 的存在，以網頁來講，它再造訪這個網頁時會留下 Cookie，而當你再次造訪時它會再次回傳到使用者的瀏覽器。

Cookie 會幫你把在網站上打得一些文字記錄下來，例如帳號密碼。也能利用它記錄用戶的習慣，利用這些信息打造用戶個性化的服務。例如：廣告商追蹤用戶 -> 看手錶的網站就會跳出很多手錶廣告...之類。

**Cookie** 特點：
* 資料儲存量：4 KB左右。
* 生命期： 可自訂失效的時間，默認是關閉瀏覽器後失效。
* 儲存位置：Browser and Server.
* 是否隨著 http req/res：Yes.


## Session Storage、Local Storage

locaol Storage 是由 html5 所提供的一個 web storage，擁有5MB的大小，可供程式設計者使用。

Session Storage 跟 Local Storage 很相似，不同的是 Local Storage 會永久保存；Session Storage 在關閉頁面或瀏覽器後就會被清除。

Local Storage 現在可以代替 Cookie 管理購物車的工作，同時也能勝任其他一些工作。比如 HTML5 遊戲通常會產生一些本地數據，Local Storage 也是非常適用的。

**Session Storage** 特點：
* 資料儲存量：5 MB左右。
* 生命期：關閉頁面或瀏覽器後。
* 儲存位置：瀏覽器。
* 是否隨著 http req/res：No.

**Local Storage** 特點：
* 資料儲存量：5 MB左右。
* 生命期：永久保存，除非被清除
* 儲存位置：瀏覽器。
* 是否隨著 http req/res：No.