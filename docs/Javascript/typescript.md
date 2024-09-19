---
layout: default
title: Typescript
parent: Javascript
nav_order: 5
---

# Typescript

자바스크립트의 수퍼셋 타입스크립트 타입이 있어서 더 좋은거라고...? 맞긴한데 타입스크립트는 C보다도 더러운 느낌이 든다. 그냥 그렇다구

## 2024_09_15

### FormData 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴 이건 사실 자바스크립트 봐야할듯 책보고 익히자

자바스크립트 단에서 폼데이터를 다루는 객체라고 한다. 흠 왜 이걸 모르고있었지 싶다.

key value 값으로 추가해준다!

```js
formData.append(name, value);
// - form의 name 과 value 를 필드의 추가
// - input의 name 속성과 value 입력값 역할을 한다고 생각 하면 된다.

formData.append(name, blob, fileName);
// - input 의 type 이 'file' 인 경우에 사용
// - fileName은 file의 이름의 해당

formData.delete(name);
// - 주어진 name 으로 필드를 제거

formData.get(name);
// - 주어진 name 의 해당 하는 필드 value를 반환

formData.getAll(name);
// - append 함수로 추가시 name이 중복 가능
// - 따라서 주어진 name 의 해당 하는 필드의 모든 value를 반환

formData.has(name);
// - 주어진 name 의 해당하는 필드가 있을 경우 true, 없으면 false를 반환

formData.set(name, value);
formData.set(name, blob, fileName);
// - set 함수는 append 함수 처럼 필드를 추가
// - append와 비슷한 set 메소드는 set도 추가를 해주기는 하지만, 기존 key가 있으면 그 key값을 모두 덮어씌워버린다
```

## 2024_09_19

### `// @ts-ignore`

컴파일러에게 다음 줄의 코드에 대한 타입 검사를 무시하도록 지시하는 주석

{: .note }
당연히 남용하면 타입스크립트 사용하는 의미가 없어진다.
