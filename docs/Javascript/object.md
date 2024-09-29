---
layout: default
title: Object
parent: Javascript
nav_order: 5
---

#Object

![gorapaduck](image-2.png)

응...? 개개개개객체

## 2024_09_15

### FormData

자바스크립트 단에서 폼데이터를 다루는 객체라고 한다. 흠 왜 이걸 모르고있었지 싶다.

key value 값으로 추가해준다!

```js
let formData = new FormData();
// 새로운 객체 생성
formData.append(name, value);
// - form의 name 과 value 를 필드의 추가

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

위는 formData 메서드 몇가지이고 formData 이야기를 좀 해보려고한다.

우선 우리가 흔히 쓰던 Form 태그를 통해 보냈던 정보들을 키와 값으로 보내는 방법이다. 그러니 이제 form태그를 통해 데이터를 전송 할 필요없다 👍 물론 써야할땐 써야겠지만?

자바스크립트 클래스이기에 서버에 전송하려면 fetch를 쓰자 그리고 Content-Type은 브라우저가 자동으로 설정해주니 지정할필요가 따로 없당

```js
const response = await fetch("http://example.org/post", {
  method: "POST",
  body: formData,
});
```

_formData로 데이터보내기_

{: .warning }
`formData.append(name, value);` 이렇게 추가 할때 value는 무조건 문자열이다! 문자열이 아니면 문자열로 자체적으로 바뀐다.

{: .note }
formData는 단순한 객체가 아니다!
