---
layout: default
title: Set & Map
parent: Javascript
nav_order: 4
---

# Set

중복되지 않는 유일한 값들의 집합

```js
const set = new Set([1, 2, 3, 3]);
console.log(set); //Set(3) {1,2,3}
```

이터러블 객체를 인수로 줄수 있고 중복된 요소는 제거하고 객체에 저장한다.

```js
const uniq = (arr) => [...new Set(arr)];
console.log(uniq([1, 2, 2, 3, 4, 5, 5])); //[1,2,3,4,5]
```

이를 통해 배열에서 중복된 요소를 제거 할수있다!!! 중복요소를 제거할때 유용하게 써보자
