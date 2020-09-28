---
title: Vue：元件 (component)
date: 2020-07-11 15:33:34
tags:
  - JavaScript
  - Vue
categories: 
  - Vue
---

# Vue 元件

* 元件資料與外層的資料是分別的。

## 為什麼需要元件？

* 避免單一檔案過大
* 在很多檔案當中都可以拉出來重複使用、管理方便

<!--more-->

## 元件定義方式

### 全域註冊

全域註冊： 不管有沒有使用到這個元件，只要用到全域註冊它都會直接載入，因此全域註冊會把沒用到的組件也一起載進來，會拖累載入速度。

```
// 全域註冊
<div id=”app”>
    <global-component></global-component>
</div>

<script>
Vue.component("global-component", {
  template: `<div>{{text}}</div>`,
  data(){
    return{
      text:'我是全域註冊'
    }
  }
});

const app = new Vue({
  el: "#app"
});
</script>
```

### 區域註冊

因為全域註冊的缺點，想當然爾就會出現解決的方案啦！

區域註冊：針對特定的實體設計就能夠用區域註冊，註冊在需要它的組件當中。

```
//區域註冊
<div id=”app”>
    <gloval-component></gloval-component>
</div>

<script>
const app = new Vue({
  el: "#app",
  components:{
    'gloval-component' :{
       template: `<div>{{text}}</div>`,
       data(){
         return {
          text:'我是局部註冊'
         }
       }
     }
  }
});
</script>
```


## 元件資料傳遞

進入元件後所有 data 都必須用 function return。

```
//如果元件的資料不用 function 回傳會讀取不到資料喔！
Vue.component('名稱', {
    template: `<div>{{text}}</div>`,
    data() {
        return {
            data: {
                text: ''
            }
        }
    }
})
```