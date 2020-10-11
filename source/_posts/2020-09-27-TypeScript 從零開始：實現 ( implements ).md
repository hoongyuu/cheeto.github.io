---
title: TypeScript 從零開始：實現 ( implements )
date: 2020-09-27 18:17:00
tags:
  - TypeScript
categories: 
  - TypeScript
---

# TypeScript 從零開始：實現 ( implements )

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FXZBuk51.png?alt=media&token=190cc704-893e-4dea-ac8c-65043a94280d)

TypeScript 是 JavaScript 的超集合，將強型別帶入 JavaSript，並提供對 ES6 的支援，而 TypeScript 由 Microsoft 開發，程式開源於 **GitHub** 上。

> 學習資源參考 [TypeScript 新手指南](https://willh.gitbook.io/typescript-tutorial/)

<!--more-->

# 實現 ( implements )

在 TypeScript 中類別可以透過 `implements` 來加入 `interface` 的作用。 

來看看一個簡單的範例：

```
interface Bark {
  bark(): any;
}

class Animal {
}

class Dog extends Animal implements Bark {
  bark() {
    console.log('吠叫汪汪');
  }
}
```

透過 `implements` 加入 `Bark` 之後，如果裡面沒有 `bark` 這個方法，那 TS 將會無情給你一個錯誤提示。

接下來看看一個類別實現多個介面：

```
interface Bark {
  bark(): any;
}

interface Basic {
  move(): any;
  stop(): any;
}

class Animal {
}

class Dog extends Animal implements Bark, Basic {
  bark() {
    console.log('吠叫汪汪');
  }
  move() {
    console.log('移動');
  }
  stop() {
    console.log('停止移動');
  }
}
```

## 介面繼承

介面也能夠繼承與介面繼承：

```
interface Bark {
  bark(): any;
}

interface Basic extends Bark {
  move(): any;
  stop(): any;
}
```

只需要這樣 `Basic` 就能夠繼承到 `Bark`

<br>

當然在類別實現介面時，只需要實現一個 `Basic` 就好了：

```
interface Bark {
  bark(): any;
}

interface Basic extends Bark {
  move(): any;
  stop(): any;
}

class Animal {
}

class Dog extends Animal implements Basic {
  bark() {
    console.log('吠叫汪汪');
  }
  move() {
    console.log('移動');
  }
  stop() {
    console.log('停止移動');
  }
}
```