---
layout: default
title: Array
parent: Javascript
nav_order: 1
---

# Array

### Array.from

유사배열 객체와 이터러블 객체를 인수로 전달하면 배열로 변환하는 매서드이다.

```js
Array.from({ length: 2, 0: "a", 1: "b" }); // -> ['a','b']

Array.from("hello"); //->['h','e','l','l','o']

Array.from({ length: 3 }, (_, i) => i); //->[0,1,2]
```
