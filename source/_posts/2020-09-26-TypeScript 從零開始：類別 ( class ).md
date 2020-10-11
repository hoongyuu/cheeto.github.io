---
title: TypeScript 從零開始：類別 ( class )
date: 2020-09-26 18:17:00
tags:
  - TypeScript
categories: 
  - TypeScript
---

# TypeScript 從零開始：類別 ( class )

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FXZBuk51.png?alt=media&token=190cc704-893e-4dea-ac8c-65043a94280d)

TypeScript 是 JavaScript 的超集合，將強型別帶入 JavaSript，並提供對 ES6 的支援，而 TypeScript 由 Microsoft 開發，程式開源於 **GitHub** 上。

> 學習資源參考 [TypeScript 新手指南](https://willh.gitbook.io/typescript-tutorial/)

<!--more-->

# 類別 ( class )

## public ( 公有 ) 與 private ( 私有 )

`public` 是公有的方法，任何時候都可以被訪問到，預設的方法與屬性也都會是公有的。

```
class Person {
  public name;
  public constructor (name: string) {
    this.name = name;
  }
}
const fufu = new Person('富富');
console.log(fufu.name); // 富富
```

在正常的情況下都能 `fufu.name` 都是可以被呼叫及訪問的，接下來讓我們看看 `private`。

```
class Person {
  private name;
  public constructor (name: string) {
    this.name = name;
  }
}
const fufu = new Person('富富');
console.log(fufu.name); // 報錯：Property 'name' is private and only accessible within class 'Person'.
```

`private` **可以把屬性或方法定義為私有的**，所以不能在宣告它的類別外部訪問。

```
class Person {
  private name;
  public constructor (name: string) {
    this.name = name;
  }
  public sayHi () {
    console.log(`${ this.name } 說你好`); // 在類別內部呼叫可以，但是無法在外部進行訪問及呼叫。
  }
}
const fufu = new Person('富富');
console.log(fufu.sayHi()); // 富富 說你好
```

可以看到在 `sayHi()` 的方法裡把 `name` 取出來是不會跳錯的，所以 `private` 是無法進行外部訪問的。

## protected ( 保護 )

上面介紹了 public ( 公有 ) 與 private ( 私有 )，那 protected ( 保護 ) 與他們的差別在於，`protected` 可以被實例呼叫。

```
class Animal {
  protected family;
  public constructor (family: string) {
    this.family = family;
  }
}

class Dog extends Animal {
  constructor (family: string) {
    super(family);
  }
  callFamily () {
    console.log(this.family);
  }
}

const fufu = new Dog('小狗');
fufu.callFamily(); // 小狗
console.log(fufu.family); // 報錯：Property 'family' is protected and only accessible within class 'Animal' and its subclasses.
```

可以看到 `Animal` 的實例中 `Dog` 是有辦法訪問到 `family` 這個屬性的，但是 `family` 卻是無法被外部進行訪問的！

## readonly ( 唯讀 )

顧名思義就是沒辦法被更改，只允許被讀取的一個修飾符。

```
class Animal {
  readonly family;
  public constructor (family: string) {
    this.family = family;
  }
}

const fufu = new Animal('小狗');
fufu.family = '小貓'; // 報錯：Cannot assign to 'family' because it is a read-only property.
```

## abstract ( 抽象類別 )

抽象類別有點類似 介面 ( interface )，接下來就繼續介紹吧！

抽象類別是不能被實體化的：

```
abstract class Person {
  public name;
  public constructor (name: string) {
    this.name = name;
  }
  abstract sayHi (): string;
}

const fufu = new Person('富富'); // 報錯：Cannot create an instance of an abstract class.
```

報錯內容顯示不能再抽象類別實體化，所以跳出這個錯誤。

所以說抽象類別一定要有子類別去繼承才能實體化：

```
abstract class Person {
  public name;
  public constructor (name: string) {
    this.name = name;
  }
  public abstract sayHi (): string;
}

class Fufu extends Person {
  public constructor (name: string) {
    super(name);
  }
}

const fufu = new Fufu('富富');

// 報錯：Non-abstract class 'Fufu' does not implement inherited abstract member 'sayHi' from class 'Person'.
```

這邊就要解釋一下了，上面有說實體化有點類似 `interface`，所以被 `abstract` 定義的屬性或方法就一定要在子類別中被定義才行，不然就會跳出這樣的錯誤唷！

```
abstract class Person {
  public name;
  public abstract hair: string;
  public constructor (name: string) {
    this.name = name;
  }
  public abstract sayHi (): string;
}

class Fufu extends Person {
  public hair = '黑色';
  public constructor (name: string) {
    super(name);
  }
  public sayHi () {
    return 'Hello World!';
  }
}

const fufu = new Fufu('富富');
```

只要我們把 被 `abstract` 定義的屬性或方法都定義到子類別，那 TypeScript 就不會再跳出任何錯誤了。