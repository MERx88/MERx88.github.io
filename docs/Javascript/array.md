---
layout: default
title: Array
parent: Javascript
nav_order: 2
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

### Arrray.prototype.slice 메서드

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

### Arrray.prototype.indexOf

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
