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

## String.prototype.search

인수로 전달받은 정규표현식과 매치하는 문자열을 검색하여 일하는 문자열의 인덱스를 반환

**특징**

1. 검색 실패 -> -1

```js
const string = "oh hello jang";

string.search(/e/); //4

string.search(/y/); //-1
```

## String.prototype.substring

두개의 인수를 받으며 첫번째 인수 인덱스 부터 두번째 인수의 인덱스 바로전까지 반환하는 메서드다

```js
const string = "oh hello jang";

string.substring(1, 4); //'h h'
```

**특징**

1. 두번째 인수 생략시 -> 첫번쨰 인수 인덱스 부터 끝까지 반환

2. 특이 케이스
   - 첫번째 인수 > 두번째 인수 -> 두 인수가 교체되어 메서드 작동
   - 인수 < 0 or NaN 이면 0으로 취급
   - 인수 > 문자열 길이 -> 인수를 문자열 길이와 동일하게 취급

## String.prototype.slice

String.prototype.substring과 동일하게 작동한다. 한가지 다른 점은 음수인 인수를 받을수 있다.

```js
const string = "oh hello jang";

string.slice(-4); //'jang'
```

## String.prototype.indexOf

String.prototype.substring과 동일하게 작동한다. 한가지 다른 점은 음수인 인수를 받을수 있다.

```js
const string = "oh hello jang";

string.slice(-4); //'jang'
```
