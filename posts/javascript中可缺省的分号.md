---
title: javascript中可缺省的分号
date: 2021-04-17 13:02:26
tags: javascript,大犀牛学习日记
---

写javascript的都知道，代码中的分号(;)很多时候都可以省略不写的，原因是javascript的解析器能够自动的分隔语句。

例如，如果两条语句分别在两行，通常分号是可以被省略的，或者一条语句的接下来是右花括号 }，那么这里的分号也可以省略的。但是有些情况下的分号是必须的，比如如下代码：

``` javascript
a = 3; // 这里的分号可以省略
b = 4; // 这里的分号可以省略

c = 3; d = 4; // 这里的第一个分号是必须的
```

注意，javascript中并不是每一次的换行都会被当作分号，而是在不隐式的添加分号就无法解析代码的时候，才会加上分号，否则不会自动添加分号。例如，一下代码：

``` javascript
let a
a
=
3
console.log(a)
```

javascript解析器会将代码理解为：
``` javascript
let a; a = 3; console.log(a)
```

javascript解析器在没有显性的分号时，会尽量的解析更长的代码，直至无法正确解析时，才会隐形的添加分号。

因为如上原因，那么就会造成以下情况：
``` javascript
let y = x + f
(a + b).toString()
```

程序员的本意可能时，这里是两个语句，但是javascript会理解为
```javascript
let y = x + f(a + b).toString(); // 解析器会尽可能的理解更长的语句
```

以上的这种情况，程序员的真实意图与javascript解析器解析出来的结果完全不一致，这种情况的问题，若果不注意，是很难发现的。

所以，有些情况下就会出现防御性的分号，还用上一个例子演示。
``` javascript
let y = x + f
;(a + b).toString() // 这里的分号是一个防御性的分号，通常会出现在()或[]开头的语句中，比如;[1,2,3].join(',')
```

上面说到，javascript会尽可能的理解更长的语句，但是涉及到return，throw，yield，break和continue语句时，则不然，若以上语句后面没有显性的分号且跟着换行符，解析器则会自动分隔语句，例如：
``` javascript
return
true;
```
javascript理解为

``` javascript
return;
true;
```

这意味着，一定不能在return，break或continue等关键字后面的表达式之间加入换行符。