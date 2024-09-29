---
layout: default
title: Kick off
parent: Algorithm
nav_order: 1
toc: true
---

# Kick off

그저 이제 시작하는... 범부

프로그래머스 입문 문제로 기초 다지기

---

## Table of contents

- [2024_08_08](#2024_08_08)
- [2024_08_10](#2024_08_10)
- [2024_08_11](#2024_08_11)
- [2024_08_21](#2024_08_21)
  - [구슬을 나누는 경우의 수](#구슬을-나누는-경우의-수)
- [2024_08_22](#2024_08_22)
  - [문자열 정렬하기 (1)](#문자열-정렬하기-1)
- [2024_08_23](#2024_08_23)
  - [합성수 찾기](#합성수-찾기)
- [2024_08_24](#2024_08_24)
  - [중복된 문자 제거](#중복된-문자-제거)
- [2024_08_25](#2024_08_25)
  - [진료순서 정하기](#진료순서-정하기)
- [2024_08_27](#2024_08_27)
  - [모스부호 (1)](#모스부호-1)
- [2024_09_01](#2024_09_01)
  - [숨어있는 숫자의 덧셈](#숨어있는-숫자의-덧셈)
- [2024_09_03](#2024_09_03)
  - [k의 개수](#k의-개수)
- [2024_09_12](#2024_09_12)
  - [한 번만 등장한 문자](#한-번만-등장한-문자)
- [2024_09_13](#2024_09_13)
  - [A로 B 만들기](#A로-B-만들기)

---

## 2024_08_08

시작...
근데 블로그 만드는 거 왤캐 빡세냐;;;

---

## 2024_08_10

블로그를 시작하기 전 공부했던 알고리즘에서 배운 개념과 자바스크립트 문법 정리

[Arrray.prototype.sort Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

[Arrray.prototype.push Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

[Arrray.prototype.splice Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

## 2024_08_11

8_10에 이어서 블로그를 시작하기 전 공부했던 알고리즘에서 배운 개념과 자바스크립트 문법 정리

[Arrray.prototype.includes Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

### 문자열! String!

텍스트 데이터를 나타낼때 사용되며 일반적인 표기는 ('') 작은 따옴표로 감싸는 것!

**문자열은 변경불가능한값이다**

{: .highlight }
🧐 근데 의문인점... 변경 불가능이라면서 아래 처럼 추가는 어떻게 되는거지...?

```js
let my_string = "B";
console.log((my_string += "A")); //'BA'
```

문자열 변경불가능에 대해 찾아보다가 자바스크립트의 값이 어떻게 할당되는지 명확히 할필요가 있어보여 이에 대해 명확히하고 넘어가고자 살펴보았다.
[값의 할당 Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

또 더 찾아보다가 원시타입과 객체타입을 확인하게 되었는데 기존의 데이터 타입에 대한 개념도 명확히 하고자 정리를 한번더 진행했다.
[원시 타입과 객체 타입 Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

{: .highlight }
🧐 인덱스 -1은 사용할수없는가...?

C언어나 다른 배열에서 -1을 사용하여 마지막 요소를 찾을 수 있는데 왜 못찾을까 했는데 쟈스 배열은 객체라는 사실 때문에 못찾았던 것이다 자세한건 아래 링크에 정리했다.
[쟈스 배열 Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

## 2024_08_21

{: .note }
`Math.round` ->소수점 이하를 반올림하는 메서드

### 구슬을 나누는 경우의 수

코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

https://school.programmers.co.kr/learn/courses/30/lessons/120840

조합 공식을 통해 공을 뽑는 경우의 수 구하기 문제

내 생각

- 팩토리얼은 재귀함수로 구현한다.

생각하지 못한 것

- 공의 갯수와 뽑아야 하는 갯수가 같은 경우 -> 이경우는 1이다. 예외를 생각하지 못했다.

궁금한 것

- Math.round 라는 메서드를 사용해야 풀리는데 왜일까?
  => 10진수의 소수를 2진수로 표현하는데 무한소수 현상이 발생해서 값이 미세하게 달라질수있다. (10진수 소수를 2진수 소수로 바꿀때 저장공간의 한계로 값이 달라진다.)
- 그리고 왜 분모를 ()로 감싸줘야 풀릴까? -> 이건 사실 당연한거다 나누고 곱하면 당연히 값이 달라지지...빡대갈아

## 2024_08_22

### 문자열 정렬하기 (1)

코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

문자열에서 숫자만 뽑아 오름차순으로 정렬하는 문제

**새롭게 안 사실**

- 문자앞에 +를 붙이면 타입이 number로 바뀐다 이런식으로 '1' -> 1 좀더 확장하면 산술연산자가 붙으면 number로 강제 형변환이 되는거 같다

- `isNaN()` : 숫자가 아니면 true를 반환한다. (is not number?) string 숫자 , number 숫자 모두 false를 반환한다!

## 2024_08_23

### 합성수 찾기

코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

주어진 n이하의 수중에서 합성수 갯수를 찾는 문제

**내 생각**

- 우선 합성수를 구하는 공식을 모른다.
- 그렇다면 합성수의 조건을 내가 띵킹하는 수밖에
- 합성수는 1이외의 어떤 수로도 나뉘면 안됨!
- 근데 제한 범위가 100미만이네? -> 오케이 그러면 2,3,5,7 이 숫자 네개로 나누면 나머지가 0이 되는 수는 합성수
- 그냥 조건 네개 걸자!

**생각하지 못한 것**

- 2,3,5,7 이 세가지는 예외 케이스로 두어야한다. 이친구들은 당연히 나누면 나머지가 0이니까 소수인데 합성수로 판별해버리면 클남

**다른 사람 풀이 해석**

```js
function solution(n) {
  let dp = new Array(n + 1).fill(1);
  for (let i = 2; i <= n; i++) {
    if (dp[i]) {
      for (let j = 2; i * j <= n; j++) {
        dp[i * j] = 0;
      }
    }
  }

  return dp.filter((el) => el === 0).length;
}
```

- 우선 1로 전부 채운다.
- 내가 선택한 인덱스의 배수는 전부다 0으로 바꾸는 방법이다 이중 반복문을 통해 진행한다. 1이 0으로 바뀌기 때문에 이미 합성수로 판별난 애들 예를 들어 4같은 애들은 두번쨰 반복문을 돌필요가 없어진다.
- 그리고 0인애들만 살려서 배열 길이를 반환한다.

_👍 개쩐다_

**또 다른 풀이 해석**

```js
function solution(n) {
  let answer = 0;
  for (let i = 1; i <= n; i++) {
    let count = 0;
    for (let j = 1; j <= i; j++) {
      if (i % j === 0) {
        count++;
      }
    }
    if (count >= 3) answer++;
  }
  return answer;
}
```

결국 나보다 작은 1을 제외한 수로 나누었을때 0이 되면 합성수 이다. 그렇기 때문에 나누는 수가 나머지를 0으로 만들때 이 갯수가 3이상이 되면 무조건 합성수 이다. 이를 활용한 풀이법이다. 제일 베이직한거 같다.

## 2024_08_24

### 중복된 문자 제거

코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

https://school.programmers.co.kr/learn/courses/30/lessons/120840

중복된 문자를 문자열에서 제거하는 문제

내 생각

- 처음에는 filter를 이용하고자 했지만 첫번째 중복 문자는 살려야하기 때문에 올바르지 않음
- 그래서 그냥 이중 중복문으로 splice 로 제거 하고자 함

문제점

- 문자열을 제거할때마다 j-- 를 해줘야한다. -> 그 이유는 문자열이 줄어들면서 다음 체크해야할 단어를 뛰어 넘고 진행하기 때문에 문제가 생긴다. 예를 들어 문자 'abaacdf'를 돌리면 무조건 a가 두개 남을것이다. 연속적으로 되어있으면 체크를 안하고 넘어가기 때문이다. 주의 하자

출제의도(?)

- set을 알고 있는가?를 묻는 문제인거 같다.
- set은 중복된 요소는 허용하지 않기 때문에 중복된 요소를 제거하기 좋다.

**Set이란?**
[Set Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

## 2024_08_25

### 진료순서 정하기

코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

https://school.programmers.co.kr/learn/courses/30/lessons/120835/solution_groups?language=javascript

부상의 정도를 보고 이를 우선순위로 바꾸는 문제

**내 생각**

- 우선순위 정렬된 배열과 정렬되지 않은 기존 배열을 비교해서 정렬된 배열 요소의 인덱스를 차례로 넣어주면 되지않을까 생각함
- 이중 반복문을 사용하기에 시간복잡도 면에서 아쉽다.

**문제점**

- 배열을 다른 배열에 할당할때 얕은 복사가 되므로 다른 배열을 수정하면 기존배열이 수정된다... -> `[...emergency]`그래서 다음과 같이 스프레드해주었다.

**다른 사람 풀이**

```js
function solution(emergency) {
  let sorted = emergency.slice().sort((a, b) => b - a);
  return emergency.map((v) => sorted.indexOf(v) + 1);
}
```

- 이중 반복문을 사용할필요가 없었다. 사실 indexOf 를 사용하면 잘 풀릴걸 알고있었지만 사용법을 잘몰랐던거 같다.
- 그리고 slice를 쓰는데 `[...emergency]` 처럼 깊은 복사를 위해 사용되었다고 한다. slice도 자세히 알아보자
- 그래도 접근법은 비슷하다!

**indexOf이란?**
[indexOf Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

**slice란?**
[slice Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

## 2024_08_27

### 모스부호 (1)

코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

https://school.programmers.co.kr/learn/courses/30/lessons/120838

모스부호를 문자로 바꾸는 문제

**짚고 넘어갈 것**

- 문제를 풀면서 큰문제는 없었는데 split이 생각이 안나서 반복문으로 띄어쓰기를 찾아서 나누어주며 풀었다.
- 조금더 구동원리를 파악하며 풀자! -> 물론 변수를 잘못봐서 살짝 헤메긴했다

**split이란?**
[split Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

## 2024_09_01

### 숨어있는 숫자의 덧셈

코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

![botchi...hard2...!!!!!!!!!](https://i.pinimg.com/564x/89/06/de/8906dec57542658ad290810b21f5475d.jpg)

https://school.programmers.co.kr/learn/courses/30/lessons/120864

문자열에서 숫자를 찾아 더하고 이를 반환하는 문제

{: .note }
한줄로 풀고 싶어서 내가 알고있는 배열 메소드 이것저것 생각하다가 시간끌다가 도저히 안되겠다 싶어서 하드하게 풀어버렸다... 근데 다른 사람들은 이걸 어떻게 한줄로 푸는거지 했는데 아직 내가 생각하지 못하는 메소드가 너무 나도 많고 아직 실력이 부족하다.

**내 코드**

```js
function solution(my_string) {
  const num_arr = ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0"];
  let fin = [];
  let answer = 0;

  for (i = 0; i < my_string.length; i++) {
    let arr = [];

    while (num_arr.includes(my_string[i])) {
      arr.push(my_string[i]);
      i++;
    }

    if (arr.length) {
      fin.push(arr);
    }
  }

  for (i = 0; i < fin.length; i++) {
    answer += +fin[i].join("");
  }
  return answer;
}
```

**내 생각**

- 이 문제에서 중요하게 여겨할건 자연수가 이어져있으면 하나의 자연수라는거다 예를들어 "a1nd23fg" 이라면 여기서 자연수는 1과 23 이다 즉 합하면 24이다.
- 그렇다면 배열을 돌다가 숫자를 만나면 배열에 저장해두고 이걸 최종배열에 저장해두면 (이중배열) 숫자는 걸러진다. -> n^2
- 그러고 이걸 다시 반복문을 돌아 더하면? -> 완료

**짚고 넘어갈거**

- 문자앞에 +를 붙여야 숫자로 변한다 명심하자 유용하다

**문제점**

- 정규표현식을 한번 봐야겠다 솔직히 안쓰고 풀고싶은데 알면 한줄로 푸는데 유용해진다.
- 공간복잡도도 최대한 줄여바야겠다.
- 아직 모르는 베열 메소드가 많다 -> 몇개 정리하면서 다른 사람 풀이를 보자

**다른 사람 풀이**

우선 reduce를 쓰는 사람이 많아서 이를 정리하고 넘어가려한다.

- **reduce이란?**
  [reduce Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

```js
function solution(my_string) {
  return my_string.split(/\D+/).reduce((acc, cur) => acc + Number(cur), 0);
}
```

알고 보면 겁나 간단하다.

1. split과 정규표현식을 통해 숫자만으로 이루어진 배열 반환 `\D+`는 숫자가 아닌 연속된 문자열 이라는 정규표현식이다.
2. reduce를 통해 숫자로만 된 배열 다 더하기 이때 Number로 형변환

**다른 사람 풀이 2**

```js
function solution(my_string) {
  return my_string
    .replace(/[A-z]/g, " ")
    .split(" ")
    .map((v) => v * 1)
    .reduce((a, b) => a + b);
}
```

- **replace란?**
  [replace Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

ex) 'ab12c2n'

1. replace로 영어는 모두 ' '로 대체한다. -> ' 12 2 '
2. split으로 모두 나눈다. -> ['','','12','',2,'']
3. map으로 새로운 배열을 만드는데 문자열 배열을 숫자 배열로 바꾸는 과정이다.[0,0,12,0,2,0]
4. reduce를 통해 모든 숫자를 더한다.

## 2024_09_03

### k의 개수

코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

https://school.programmers.co.kr/learn/courses/30/lessons/120887

주어진 범위 내에서 k의 갯수를 구하는 문제

🤩 좀 신박한 풀이법을 봐서 적어두고 가고자 한다.

**다른 사람 풀이**

```js
function solution(i, j, k) {
  let a = "";
  for (i; i <= j; i++) {
    a += i;
  }

  return a.split(k).length - 1;
}
```

- 우선 하나의 문자열로 만드는 반복문 체크!
- split의 활용도가 특이한데 해당 k로 문자열을 쭉 나누면 아래와 같이 나오는데 생각해보면 k 갯수에서 항상 +1 한값이 나온다는 것을 확인할수있다.

👍 역시 천재들!

```
12345678910111213
[ '', '23456789', '0', '', '', '2', '3' ]
```

## 2024_09_12

### 한 번만 등장한 문자

코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

https://school.programmers.co.kr/learn/courses/30/lessons/120896

한번만 등장한 문자들을 모아 문자열로 리턴하는 문제

**내 생각**

- filter와 reduce를 조합하면 문제를 풀수있지 않을까 생각함 요소를 하나씩 filter에서꺼내고 이를 reduce에 넘겨주어 몇번 등장했는지 체크했는지 보고 다시 filter에서 대소비교를 해서 2보다 작으면 해당 엘리먼트를 배열에 담는 그러한 방법

**문제점**

- 메소드 사용의 미숙함
  - reduce는 return을 써줘야하며 중괄호 사용도 가능하다
  - filter는 소괄호만 사용가능하다.

```js
function solution(s) {
  return [...s]
    .filter(
      (el) =>
        [...s].reduce((acc, cur) => {
          return cur == el ? acc + 1 : acc;
        }, 0) < 2
    )
    .sort()
    .join("");
}
```

## 2024_09_13

### 🚧🚧 A로 B 만들기 🚧🚧

코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

![botchi...hard...!!!!!!!!!](https://i.pinimg.com/564x/8e/fa/be/8efabe8d7388409a200fdd8fa69e6530.jpg)

https://school.programmers.co.kr/learn/courses/30/lessons/120896

한번만 등장한 문자들을 모아 문자열로 리턴하는 문제

**내 생각**

**문제점**

```js

```

## 2024_09_28

### 🚧🚧 영어가 싫어요 🚧🚧

🚧 ...작성중... 🚧
{: .label .label-yellow }
코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

https://school.programmers.co.kr/learn/courses/30/lessons/120896

영어 문자열을 숫자로 바꾸는 문제 ex. zerotwo -> 02

**내 생각**

그냥 요소 돌면서

- 하나씩 배열에 집어넣고 이 배열을 통째로 체크
  -> 있다면 숫자로 변환 그후 배열 초기화
  -> 없다면 다시 배열에 넣는 작업

**내 코드**

```js
function solution(numbers) {
  const text_arr = [
    "zero",
    "one",
    "two",
    "three",
    "four",
    "five",
    "six",
    "seven",
    "eight",
    "nine",
  ];
  let temp_arr = [];
  let answer = [];
  const number_arr = [...numbers];
  number_arr.forEach((el) => {
    temp_arr.push(el);
    if (text_arr.includes(temp_arr.join(""))) {
      answer.push(text_arr.indexOf(temp_arr.join("")));
      temp_arr = [];
    }
  });
  return +answer.join("");
}
```

**문제점**

-

**처음 알게 된 사실**

- 스프레드 문법 하고 바로

```js

```
