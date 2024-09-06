---
layout: default
title: Array
parent: Javascript
nav_order: 2
---

# Array

배열인척하는 미친 객체 녀석의 드럽게 많은 배열 메소드 정리 페이지

## Table of contents

- [Array.from](#arrayfrom)
- [Arrray.prototype.sort](#arrrayprototypesort)
- [Arrray.prototype.push](#arrrayprototypepush)
- [Arrray.prototype.splice](#arrrayprototypesplice)
- [Array.prototype.unshift](#arrrayprototypeunshift)
- [Arrray.prototype.includes](#arrrayprototypeincludes)
- [Arrray.prototype.slice](#arrrayprototypeslice)
- [Arrray.prototype.indexOf](#arrrayprototypeindexOf)
- [Arrray.prototype.forEach](#arrrayprototypeforEach)
- [Arrray.prototype.map](#arrrayprototypemap)
- [Arrray.prototype.reduce](#arrrayprototypereduce)
- [Arrray.prototype.replace](#arrrayprototypereplace)

---

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

## Arrray.prototype.push

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

## Arrray.prototype.unshift

**특징**

1. 인수로 받은 값을 제일 처음요소로 추가한다. 즉, 원본 배열이 수정된다.
2. 변경된 배열의 길이(length)를 반환한다.

```js
const arr = [1, 2];

let result = arr.unshift(3, 4);

console.log(result); //4

console.log(arr); //[3,4,1,2]
```

## Arrray.prototype.splice

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

## Arrray.prototype.includes

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

## Arrray.prototype.slice

인수로 전달된 범위의 요소들을 복사하여 배열로 반환한다

**특징**

1. 원본 배열을 바꾸지 않는다 ( ⭐️ splice는 원본배열 변경한다.)

`arr.slice(start, end);`

start : 복사를 시작할 인덱스!

end : 어디까지 복사할지 정하는 인수

```js
const arr = [1, 2, 3];

arr.slice(0, 1); // [1]

arr.slice(-2); // [2,3]

arr.slice(1); // [2,3]

const copy = arr.slice(); //앝은 복사를 통해 복사본을 생성한다.

console.log(copy); //[1,2,3]
```

위와 같이 다양하게 사용할수있다.

{: .highlight }
🧐 근데 의문인점... 얕은 복사라면 arr을 바꾸면 copy에도 영향이 가는거 아닌가?...? 왜 깊은복사 같이 움직이지

[배열이 종류에 따른 복사 - 누군가가 잘정리해줌~ Link](https://velog.io/@y_jem/javascript-slice%EA%B0%80-1%EC%B0%A8%EC%9B%90-%EB%B0%B0%EC%97%B4%EC%9D%80-%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC-2%EC%B0%A8%EC%9B%90-%EB%B0%B0%EC%97%B4%EC%9D%80-%EC%96%95%EC%9D%80-%EB%B3%B5%EC%82%AC%EB%A5%BC-%EC%88%98%ED%96%89%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0)

우선 결론부터 말하자면 요소가 원시값일 경우는 깊은복사와 같이 새로운 배열을 만들고 다른 참조를 가진다! 근데 만약 요소가 원시값이 아닌 참조값일 경우? 이때는 얕은 복사와 같이 참조가 동일하기 떄문에 서로가 영향을 미친다.

그냥 간단하게 생각해보자

```js
//원시 값은 깊은 복사가 된다.
var a = 1;
var b = a;
a = 2;
console.log(a); //2
console.log(b); //1

//참조값은 얕은 복사가 된다.
var a = [1, 2, 3];
var b = a;
a.push(4);
console.log(a); //[ 1, 2, 3, 4 ]
console.log(b); //[ 1, 2, 3, 4 ]
```

원시값은 새로운 값을 할당할때 새로운 메모리를 확보하고 이에 할당한다. 기존에도 배열은 저렇게 할당을 진행되면 참조 주소만 복사가 되었다. 이것이 그대로 slice에도 진행된다고 보면된다. 분명 앝은복사를 진행하지만 원시값은 특성상 깊은복사를 진행한다.

## Arrray.prototype.indexOf

원본배열에서 인수로 전달된 요소를 검색하여 인덱스를 반환한다.

**특징**

1. 없다면 -1을 반환
2. 여러개 존재한다면 첫번쨰로 검색된거 반환
3. 두번쨰 인덱스는 검색을 시작할 인덱스

```js
const arr = [1, 2, 3];

arr.indexOf(2); //1

arr.indexOf(6); //-1
```

## Arrray.prototype.forEach

반복문 대신 사용할수있다!

**특징**

1. 콜백함수가 배열의 요소를 받아 돌면서 처리한다.
2. forEach 메서드는 콜백함수를 호출하면서 3개의 인수를 전달한다.
   - 요소 값
   - 인덱스
   - this
3. 원본 배열을 변경하지 않는다.
   - 콜백함수를 통해 변경할수는 있다.
4. 반환값은 undefined 이다.
5. 순회를 중단 할수없다
6. 희소배열의 경우 존재하지 않는 요소는 순회대상에서 제외
7. for 문 보다 성능이 떨어지지만 가독성은 좋다

{: .note }
희소 배열이란 인덱스를 차지하고 있지만 요소가 존재하지 않은 배열 ex)`const arr=[1,,3]`

```js
[1, 2, 3].forEach((item, index, arr) => {
  console.log(`요소값: ${item}, 인덱스 ${index}, this :${JSON.stingify(arr)}`);
});
// 요소값:1, 인덱스:0, this :[1,2,3]
// 요소값:2, 인덱스:1, this :[1,2,3]
// 요소값:3, 인덱스:2, this :[1,2,3]
```

## Arrray.prototype.map

반복문 + 새로운 배열 만들기

**특징**

1. 콜백함수가 배열의 요소를 받아 돌면서 처리하고 새로운 배열을 만든다.
2. 원본 배열을 바꾸지 않는다.
3. map 메서드는 콜백함수를 호출하면서 3개의 인수를 전달한다.
   - 요소 값
   - 인덱스
   - this

```js
[1, 2, 3].map((item, index, arr) => {
  console.log(`요소값: ${item}, 인덱스 ${index}, this :${JSON.stingify(arr)}`);
  return item;
});
// 요소값:1, 인덱스:0, this :[1,2,3]
// 요소값:2, 인덱스:1, this :[1,2,3]
// 요소값:3, 인덱스:2, this :[1,2,3]
```

## Arrray.prototype.reduce

초기값(accumulator)과 배열을 가지고 콜백함수를 통해 이것 저것 할수있는 신기한 녀석

**특징**

1. acc를 주면 배열 요소들과 콜백함수를 통해 이것저것 하면서 순차적으로 진행되다가 결과값을 뱉는다
2. 즉, 하나의 결과값을 반환한다.
3. 초기값은 전달 안할수 있다 👉 _하지만 꼭 전달하자_

😇 그냥 보는게 빠르다. 예제를 좀 보자

```js
//1~4 누적값구하기
const sum = [1, 2, 3, 4].reduce(
  (accumulator, currentValue, index, array) => accumulator + currentValue,
  0
);

console.log(sum); //10
```

```js
//평균 구하기
const avr = [1, 2, 3, 4].reduce((acc, cur, i, { length }) => {
  return i === length - 1 ? (acc + cur) / length : acc + cur;
}, 0);

console.log(avr); //2.5
```

더 많은 예제가 있지만 요정도 적고 넘어가자

## Arrray.prototype.replace

초기값(accumulator)과 배열을 가지고 콜백함수를 통해 이것 저것 할수있는 신기한 녀석

**특징**

1. acc를 주면 배열 요소들과 콜백함수를 통해 이것저것 하면서 순차적으로 진행되다가 결과값을 뱉는다
2. 즉, 하나의 결과값을 반환한다.
3. 초기값은 전달 안할수 있다 👉 _하지만 꼭 전달하자_

😇 그냥 보는게 빠르다. 예제를 좀 보자

```js
//1~4 누적값구하기
const sum = [1, 2, 3, 4].reduce(
  (accumulator, currentValue, index, array) => accumulator + currentValue,
  0
);

console.log(sum); //10
```

```js
//평균 구하기
const avr = [1, 2, 3, 4].reduce((acc, cur, i, { length }) => {
  return i === length - 1 ? (acc + cur) / length : acc + cur;
}, 0);

console.log(avr); //2.5
```

더 많은 예제가 있지만 요정도 적고 넘어가자

## Arrray.prototype.replace

첫번째 인수로받은 녀석을 검색하여 두번째 인수로 받은 녀석으로 치환하는 메소드

**특징**

1. 정규표현식과 문자열로 검색가능하다
2. 만약 검색결과가 여러개일 경우 첫번쨰만 치환한다.
3. 두번째 인수로 치환함수를 전달 할수있다. 👉 일단 그렇다는것만 알아두자

```js
const str = "hello world";
str.replace("world", "lee"); //hello lee
```
