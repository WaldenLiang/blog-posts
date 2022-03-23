---
title: javascript中字符串的大小比较
date: 2021-04-17 12:04:32
tags: javascript,大犀牛学习日记
---

``` javascript
"two" > "three" // => true 按照ASCII码表进行比较，从小到大顺序：0-9A-Za-z
"a" > "99999999999999999" // => true 不论长度
```

无论长度, 从左侧开始比较。