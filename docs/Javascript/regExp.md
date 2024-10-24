---
layout: default
title: 👨‍🏫 RegExp
parent: Javascript
nav_order: 6
---

# 👨‍🏫 정규 표현식

![anya](image-5.png)

사실 챗지피티가 쓰면 뚝딱이지만 한번 정리하자 그래야 쓰지는 못하더라도 읽을 순 있으니

## 정규표현식이란?

일정한 패턴을 가진 문자열의 집합을 표현하기 위해 사용되는 형식 언어

-> 패턴 문자열 집합이라고 보면된당

이 집합으로 패턴 매칭을 한다. 패턴을 매칭해서 추출 치환 검색 등등을 할수있고 이 패턴 매칭기능이 정규표현식을 쓰는 이유와도 같다.

## 정규표현식 생성

`/regexp/i`

`/`은 시작과 종요 기호로 사용되고 그 사이에 있는 문자열 패턴을 찾는다 뒤에 붙는 문자는 플래그이다. 검색할때 설정해주는 값이라고 생각하자

```js
const target = "Is this all there is?";

const regexp = /is/i; //"is"를 찾아줘 대소문자 구분하지 말고~

regexp.test(target); //true
```

생성자 함수를 통해 RegExp 객체를 생성할수도 있다.

```js
new RegExp(pattern[,flags])
```

{ .note-title }

> nullish 병합 연산자
>
> nullish 병합 연산자(nullish coalescing operator) ??를 사용하면 짧은 문법으로 여러 피연산자 중 그 값이 ‘확정되어있는’ 변수를 찾을 수 있다.
>
> a ?? b의 평가 결과는 아래와 같다
>
> 1.  a가 null도 아니고 undefined도 아니면 a
> 2.  그 외의 경우는 b
>
> 만약 null 값이나 undefined 값이 들어올거같으면 해당 연산자를 사용해서 디폴트를 정해주자

## 정규표현식 메서드

### 🚧🚧 RegExp.prototype.exec 🚧🚧

### RegExp.prototype.test

test 메서드는 인수로 전달 받은 문자열에 대해 정규표현식 패턴을 검사해서 불리언 값으로 넘겨준다.

```js
const target = "Is this all there is?";

const regexp = /is/i; //"is"를 찾아줘 대소문자 구분하지 말고~

regexp.test(target); //true
```

### RegExp.prototype.match

대상 문자열과 인수로 전달 받은 정규표현식과의 매칭 결과를 배열로 반환!

**특징**

- 매칭되는거 전부 반환!

```js
const target = "Is this all there?";

const regexp = /is/g;

regexp.match(target); //['is', 'is']
```

## 플래그

검색 방식을 설정하는 문자이다.

| 플래그 | 의미        | 설명                                    |
| :----- | :---------- | :-------------------------------------- |
| i      | ignore case | 대소문자 구별하지 않고 패턴검색         |
| g      | global      | 패턴과 일치하는 모든 문자열을 전역 검색 |
| m      | multi line  | 행이 바뀌더라도 계속 패턴 검색          |

**특징**

- 순서와 상관없이 하나이상의 플래그를 동시 설정가능

## 패턴

정규 표현식은 일정한 규칙을 가진 문자열의 집합을 표현하기 위해 사용하는 형식 언어!

**패턴 작성법**

- 패턴은 /로 열고 닫는다.
- 문자열 따옴표는 생략한다.
- 특별한 의미를 지니는 메타 문자 또는 기호로 표현가능하다.

## 몇가지 기호들을 활용한 검색

**임의 문자열**

- `.` = 임의 문자 한개

**반복**

- `{m,n}` = 최소 m번 최대 n 번 반복되는 문자열
- `{n}` = 앞선 패턴이 n번 반복되는 문자열
- `{m,}` = 최소 m번 이상 반복되는 문자열
- `m+` = 최소 m번 이상 반복되는 문자열

- `?` = 바로 앞선 패턴이 한번 이상(0번 포함) 반복되는 문자열 의미

```js
const target = "color colour";

const regexp = /colou?r/g;

regexp.match(target); //['color', 'colour']
```

**OR**

- `m|n` = |은 or의 의미한다.
- `[mn]` = []안에 있는 문자를 or로 묶는다.
- `[m-n]`= - 로 범위를 지정할수있다.

```js
const target = "AA BB Aa Bb 12 AaA";

const regexp_char = /[A-Za-z]+/g;

regexp_char.match(target); //['AA', 'BB', "Aa", "Bb", "AaA"]

const regexp_num = /[0-9]+/g;

regexp_num.match(target); //['12"]
```

- `\D` = 숫자
- `\d`= 문자

- `\W` = `[A-Za-z0-9_]`
- `\w`= `\W` 반대로 작동

**NOT**

- `[^]` = []안의 ^은 not의 의미를 지님

**시작 위치**

- `^` = []밖의 ^은 문자열 시작을 의미

**종료 위치**

- `$` = $ 문자열 끝을 의미

```js
const target = "http://something-site.com";

const regexp_http = /^http/;

const regexp_com = /com$/g;

regexp_http.match(target); //true

regexp_com.match(target); //true
```
