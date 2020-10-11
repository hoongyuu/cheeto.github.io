---
title: TypeScript 從零開始：列舉 ( Enum )
date: 2020-09-25 14:20:00
tags:
  - TypeScript
categories: 
  - TypeScript
---

# TypeScript 從零開始：列舉 ( Enum )

![](https://firebasestorage.googleapis.com/v0/b/cheetoblog-8edf4.appspot.com/o/TypeScript%2FXZBuk51.png?alt=media&token=190cc704-893e-4dea-ac8c-65043a94280d)

TypeScript 是 JavaScript 的超集合，將強型別帶入 JavaSript，並提供對 ES6 的支援，而 TypeScript 由 Microsoft 開發，程式開源於 **GitHub** 上。

> 學習資源參考 [TypeScript 新手指南](https://willh.gitbook.io/typescript-tutorial/)

<!--more-->

# 列舉 ( Enum )

列舉 ( Enum ) 是可以快速的將多個不同的值加上名稱並群組化。

```
// 編譯前
enum Days {Sun, Mon, Tue, Wed, Thu, Fri, Sat};

let today = Days.Mon;
if (today === Days.Mon) console.log('Today is Monday');
console.log(Days.Wed);
console.log(Days.Fri === 5);

// 編譯後
var Days;
(function (Days) {
    Days[Days["Sun"] = 0] = "Sun";
    Days[Days["Mon"] = 1] = "Mon";
    Days[Days["Tue"] = 2] = "Tue";
    Days[Days["Wed"] = 3] = "Wed";
    Days[Days["Thu"] = 4] = "Thu";
    Days[Days["Fri"] = 5] = "Fri";
    Days[Days["Sat"] = 6] = "Sat";
})(Days || (Days = {}));
var today = Days.Mon;
if (today === Days.Mon)
    console.log('Today is Monday'); // Today is Monday
console.log(Days.Wed); // 3
console.log(Days.Fri === 5); // true
```

在上面的程式碼可以看到列舉的特性，可以取出**對應的值的索引值**。

## 手動賦值

在 TS 的 `enum` 可以透過手動賦值的方式來獲得更多靈活的運用。

```
// 編譯前
enum Days { 
  Sun = 'Sunday', 
  Mon = 'Monday', 
  Tue = 'Tuesday', 
  Wed = 'Wednesday', 
  Thu = 'Thursday', 
  Fri = 'Friday', 
  Sat = 'Saturday' 
}
console.log(Days.Wed);
console.log(Days.Fri);

// 編譯後
var Days;
(function (Days) {
    Days["Sun"] = "Sunday";
    Days["Mon"] = "Monday";
    Days["Tue"] = "Tuesday";
    Days["Wed"] = "Wednesday";
    Days["Thu"] = "Thursday";
    Days["Fri"] = "Friday";
    Days["Sat"] = "Saturday";
})(Days || (Days = {}));
console.log(Days.Wed); // Wednesday
console.log(Days.Fri); // Friday
```

這樣就可以迅速地取出值了，是不是也很方便呢？

## 常數列舉

常數列舉跟一般列舉的最大區別在於，程式碼過程會在編譯階段被刪除，會直接顯示編譯結果。

```
// 編譯前
const enum Days { 
  Sun = 'Sunday', 
  Mon = 'Monday', 
  Tue = 'Tuesday', 
  Wed = 'Wednesday', 
  Thu = 'Thursday', 
  Fri = 'Friday', 
  Sat = 'Saturday' 
}
console.log(Days.Wed);
console.log(Days.Fri);

// 編譯後
console.log("Wednesday" /* Wed */); // Wednesday
console.log("Friday" /* Fri */); // Friday
```

很明顯的差異出現了，在編譯後**常數列舉**會直接顯示編譯結果。