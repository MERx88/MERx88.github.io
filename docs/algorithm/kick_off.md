---
layout: default
title: Kick off
parent: Algorithm
nav_order: 1
---

# Kick off

그저 이제 시작하는... 범부

프로그래머스 입문 문제로 기초 다지기

1. TOC
   {:toc}

---

## 2024_08_08

시작...
근데 블로그 만드는 거 왤캐 빡세냐;;;

---

## 2024_08_10

블로그를 시작하기 전 공부했던 알고리즘에서 배운 개념과 자바스크립트 문법 정리

### Arrray.prototype.sort 함수

**특징**

1. 원본배열을 변경한다.
2. 기본적으로 오름차순으로 요소를 정렬한다. (유니코드 코드 포인트 기준)

```js
const fruit = ["Banana", "Orange", "Apple"];

fruit.sort();

console.log(fruit); //["Apple", "Banana", "Orange"]
```

위와 같이 영어, 한글 모두 오름차순 정렬 된다.

```js
const points = [40, 100, 1];

points.sort();

console.log(points); //[1,100,40]
```

하지만 위와 같이 숫자로 된 배열은 정렬을 할때 숫자타입을 문자타입으로 변환하고 유니코드 코드 포인트 기준으로 정렬하기 때문에 전혀 다른 결과물을 출력한다. 그렇기 때문에 숫자를 정렬할때에는 정렬순서를 정의하는 비교함수를 인수로 전달 해야한다.

```js
arr.sort((next, prev) => next - prev);
```

위와같이 비교함수를 넘겨 주면

next - prev가 0이거나 양수면 변경하사항이 없지만 음수가 되면 자리가 바뀐다.

으로 평가하여 배열을 정렬하게 된다.

```js
const points = [40, 100, 1];

points.sort((a, b) => a - b); //100-40은 양수이므로 자리가 바뀌지 않는다. 오름차순 정렬이 된다.

console.log(points); //[1,40,100]
```

```js
const points = [40, 100, 1];

points.sort((a, b) => b - a); //100-40은 양수이므로 자리가 바뀐다. 내림차순으로 정렬이 된다.

console.log(points); //[100,40,1]
```

### Arrray.prototype.push 함수

**특징**

1. 인수로 받은 값을 마지막요소로 추가한다. 즉, 원본 배열이 수정된다.
2. 변경된 배열의 길이(length)를 반환한다.
3. 성능면에서 좋지 않다.

```js
const arr = [1, 2];

let result = arr.push(3, 4);

console.log(result); //4

console.log(arr); //[1,2,3,4]
```

### Arrray.prototype.unshift 함수

**특징**

1. 인수로 받은 값을 제일 처음요소로 추가한다. 즉, 원본 배열이 수정된다.
2. 변경된 배열의 길이(length)를 반환한다.

```js
const arr = [1, 2];

let result = arr.unshift(3, 4);

console.log(result); //4

console.log(arr); //[3,4,1,2]
```

### Arrray.prototype.splice 함수 (작성중)

**특징**

1. 인수로 받은 값을 제일 처음요소로 추가한다. 즉, 원본 배열이 수정된다.
2. 변경된 배열의 길이(length)를 반환한다.

```js
const arr = [1, 2];

let result = arr.unshift(3, 4);

console.log(result); //4

console.log(arr); //[3,4,1,2]
```
