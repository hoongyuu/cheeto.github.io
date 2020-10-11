---
title: Vue：props & emit
date: 2020-07-15 15:38:34
tags:
  - JavaScript
  - Vue
categories: 
  - Vue
---

# props

props 是把資料從外層為內層傳遞的一個方法。

## props 是單向數據流

單向數據流的意思是，只能單向的從外部傳入'資料'，而不能從內部元件傳出'資料'。如果你想要這麼做的話可以使用 'emit' 來向外推送資料。

![](https://i.imgur.com/J4ec9Bz.png)

<!--more-->

```
// 利用"內層" :person 來把"外層" item 的資料帶入"內層元件"內 
<div id="app">
    <global-component v-for="(item, i) in nameData" :person="item" :key="i"></global-component>
</div>

<script>
  Vue.component("global-component", {
    // 利用 props 建立 'person' 來接收外層的資料
    props: ['person'],
    template: `<div> {{ person.name }} </div>`
  });

  const app = new Vue({
    el: "#app",
    data: {
      nameData: [
        {
          name: "小明"
        },
        {
          name: "杰倫"
        },
        {
          name: "漂亮阿姨"
        },
        {
          name: "老媽"
        }
      ]
    }
  });
</script>
```

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/Vue%2Fprops.jpg?alt=media&token=73e364d4-347b-4587-b927-7d178e07b3ca)

## props 型別

props 可以利用型別來偵錯，也能夠預設值。

[codePen](https://codepen.io/Chee7o/pen/NWxzYzK?editors=1010)

```
<div id="app">
  <prop-type :cash="cash"></prop-type>
  {{ typeof(cash)}}
</div>

Vue.component('prop-type', {
  props: {
    cash: {
    //若型別不是 Number 則會跳錯
      type: Number,
    //若 cash 為 undefined 則觸發預設值
      default: 500
    }
  },
  template: `<input type="number" v-model="newCash">`,
  data: function() {
    return {
      newCash: this.cash
    }
  }
});

const app = new Vue({
  el: '#app',
  data: {
     cash: '300'
  }
});
```

# emit

`emit` 是透過事件來對外層元件推送一個資料 ↓


![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/Vue%2Femit.jpg?alt=media&token=9b37b125-a0fb-49b0-8358-044317ec0501)