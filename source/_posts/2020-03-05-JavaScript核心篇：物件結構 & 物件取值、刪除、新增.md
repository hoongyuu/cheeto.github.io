---
title: JavaScript核心篇：物件結構 & 物件取值、刪除、新增
date: 2020-03-05 14:56:58
tags:
  - JavaScript
  - JS核心
categories: 
  - JavaScript核心篇
---


# 物件結構

建立物件有兩種方式，一種是物件實字；另一種則是物件建構式。
要設定物件的話裡面固定會有屬性跟值，屬性的名稱都會是字串不會是其他型別，值裡面可以是**字串**、**數字**、**物件**、**函式**。

## 物件實字

物件實字語法

```
var family = {
    name : '小明家',
    money: 1000,
    members: {
        mom: '老媽',
        dad: '老爸'
    },
    callFamily: function(){
        console.log('聯絡小明家');
    }
};
```

<!--more-->

## 物件建構式

物件建構式語法

```
var family = new Object();
family.name = '小明家';
family.money = 1000;
family.members = {
    mom: '老媽',
    dad: '老爸'
};
family.callFamily = function(){
    console.log('聯絡小明家');
};
```

## 物件取值

物件的取值有兩種方法，一種是用 .(點) 的方式，另一種是用 []\(中括號) 的方式。

.(點) 取值語法如下 ↓

![物件取值(點)](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%89%A9%E4%BB%B6%E5%8F%96%E5%80%BC(%E9%BB%9E).jpg?alt=media&token=ab41c454-e8af-4092-bdef-5159c6687f27)

<br>

[]\(中括號) 取值語法如下 ↓

![物件取值[]\(中括號)](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%89%A9%E4%BB%B6%E5%8F%96%E5%80%BC(%E4%B8%AD%E6%8B%AC%E8%99%9F).jpg?alt=media&token=ae18e953-a55f-4032-94f0-c25e43258418)


### 兩種取值的差異

```
var family = {
    name : '小明家',
    money: 1000,
    members: {
        mom: '老媽',
        dad: '老爸'
    },
    '1': 1,
    callFamily: function(){
        console.log('聯絡小明家');
    }
};
```

在上方程式碼如果要取出 '1' 裡面的值的話，用 .(點) 是沒有辦法取出值的

![兩種取值的差異](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E5%8F%96%E5%80%BC%E5%B7%AE%E7%95%B0.jpg?alt=media&token=1664460a-7089-4783-944b-0ca12070cc03)

另外 []\(中括號) 可以設定變數後取值。 如下 ↓

```
var family = {
    name : '小明家',
    money: 1000,
    members: {
        mom: '老媽',
        dad: '老爸'
    },
    '1': 1,
    callFamily: function(){
        console.log('聯絡小明家');
    }
};

var a = 'name';
```

![物件變數取值](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%89%A9%E4%BB%B6%E8%AE%8A%E6%95%B8%E5%8F%96%E5%80%BC.jpg?alt=media&token=ebe0d3b1-7ff0-46ac-b067-57eb91d0edc6)

### 物件新增

```
var family = {
    name : '小明家',
    money: 1000,
    members: {
        mom: '老媽',
        dad: '老爸'
    },
};

// 物件新增語法如下 ↓ 

family.dog = '小白';
family['cat'] = '點點';
```

用兩種方法都可以新增物件，這時候執行 family 會出現下面結果 ↓

![物件新增](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%89%A9%E4%BB%B6%E6%96%B0%E5%A2%9E.jpg?alt=media&token=cf9fd679-3682-467a-85e6-a7c4a8aec524)

這時候可以發現在後面依序新增了 dog 跟 cat 的屬性。

### 物件刪除

```
var family = {
    name : '小明家',
    money: 1000,
    members: {
        mom: '老媽',
        dad: '老爸'
    },
};

// 物件刪除語法如下 ↓

delete family.money;
delete family['members'];
```

用兩種方法都可以物件刪除，這時候執行 family 會出現下面結果 ↓

![物件刪除](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/JS%EF%BC%9A%E6%A0%B8%E5%BF%83%E7%AF%87%2F%E7%89%A9%E4%BB%B6%E5%88%AA%E9%99%A4.jpg?alt=media&token=992c9b8a-64fa-4f23-a450-318c30a6eefb)

這時候可以發現 money 跟 members 的屬性都不見了，只剩下了 name 的屬性。