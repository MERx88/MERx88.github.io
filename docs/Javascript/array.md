---
layout: default
title: Array
parent: Javascript
nav_order: 1
---

# Array

## Array.from

유사배열 객체와 이터러블 객체를 인수로 전달하면 배열로 변환하는 매서드이다.

```js
Array.from({ length: 2, 0: "a", 1: "b" }); // -> ['a','b']

Array.from("hello"); //->['h','e','l','l','o']

Array.from({ length: 3 }, (_, i) => i); //->[0,1,2]
```

## Arrray.prototype.sort

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

### Arrray.prototype.push

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

### Arrray.prototype.unshift

**특징**

1. 인수로 받은 값을 제일 처음요소로 추가한다. 즉, 원본 배열이 수정된다.
2. 변경된 배열의 길이(length)를 반환한다.

```js
const arr = [1, 2];

let result = arr.unshift(3, 4);

console.log(result); //4

console.log(arr); //[3,4,1,2]
```

### Arrray.prototype.splice 함수

중간에 있는 요소를 변경할때 사용한다. 하지만 중간 요소 삭제, 중간에 요소 삽입등 다양한 작업이 가능한 메소드로 꽤나 유용한거 같다

**특징**

1. 원본 배열이 수정된다.
2. 삭제된 요소를 반환한다.

`arr.splice(start, deleteCount, items...);`

start : 제거를 시작할 인덱스!

deleteCount : 제거 갯수

items : 삽입할 아이템들

```js
const arr = [1, 2, 3, 4];

let result = arr.splice(1, 2, 20, 30);

console.log(result); //[2,3]

console.log(arr); //[1,20,30,4]
```

start만 넘겨주면 그이후로 싹다 삭제된다. `let result = arr.splice(1);` 라면 arr은 [1,2]가 된다.
이외에 다양하게 응용가능하다.

### Arrray.prototype.includes 함수

뭔가 다양하게 포함을 확인할 수 있을거 같았는데 생각보다 제한적이다.

**특징**

1. boolean 값 반환

`arr.includes(검색할 대상, 검색 시작 인덱스);`

```js
const arr = [1, 2, 3, 4];

arr.splice(1); //true

arr.splice(1, 1); //false

arr.splice(4, -1); //true
```

인덱스 -1을 주게되면 length-1 값부터 확인한다.
