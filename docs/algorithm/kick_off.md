---
layout: default
title: Kick off
parent: Algorithm
nav_order: 1
---

# Kick off

{: .no_toc }

그저 이제 시작하는... 범부

프로그래머스 입문 문제로 기초 다지기

## Table of contents

{: .no_toc .text-delta }

1. TOC
   {:toc}

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

{: .d-inline-block }
코딩테스트 문제 {: .label .label-blue } 프로그래머스 {: .label .label-purple }

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

### 문자열 정렬하기 (1)

{: .d-inline-block }
코딩테스트 문제
{: .label .label-blue }
프로그래머스
{: .label .label-purple }

문자열에서 숫자만 뽑아 오름차순으로 정렬하는 문제

새롭게 안 사실

- 문자앞에 +를 붙이면 타입이 number로 바뀐다 이런식으로 '1' -> 1 좀더 확장하면 산술연산자가 붙으면 number로 강제 형변환이 되는거 같다

- `isNaN()` : 숫자가 아니면 true를 반환한다. (is not number?) string 숫자 , number 숫자 모두 false를 반환한다!
