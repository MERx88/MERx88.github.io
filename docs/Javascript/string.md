---
layout: default
title: 🆎 String
parent: Javascript
nav_order: 3
---

# String

## String.prototype.split

문자열을 인수로 받은 문자열로 구분하고 이를 배열로 반환하는 메서드

**특징**

1. 인수로 빈문자열 -> 전부다 나눔
2. 인수 없음 -> 통째로 원소가 하나인 배열

```js
const string = 'oh hello jang'

string.split(' ')=["oh","hello","jang"]

string.split('')=["o","h","h","e","l","l","o","j","a","n","g"]

string.split()=['oh hello jang']
```
