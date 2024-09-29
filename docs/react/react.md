---
layout: default
title: React
nav_order: 5
has_children: true
---

# React

아직은 잘나가는 웹프레임워크

## Re-rendering

**리렌더링이 되는 시점**

- 자신의 state가 변경될 때
- 부모 컴포넌트로부터 받아오는 props가 변경될 때
- 부모 컴포넌트가 리렌더링(re-rendering)될 때
- foreceUpdate 함수가 실행될 때 -> 강제로 다시 리렌더링 하는 함수

## 2024_09_20

### useRef🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴 사용법 부터 keep going 해야함

[react useRef](https://ko.react.dev/reference/react/useRef#useref)

"렌더링에 필요하지 않은 값을 참조할수있는 react hook" 이라고 나와 공식문서에 나와있다 의미가 뭘까 알아보자

```tsx
import { useRef } from "react";

function MyComponent() {
  const intervalRef = useRef(0);
  const inputRef = useRef(null);
  // ...
}
```

**매개변수**

- initialValue : ref 객체의 current 프로퍼티 초기 설정값이다.

**return값 (단일 프로퍼티를 가진 객체를 반환)**

- current : initialValue로 설정한 값이 초기값으로 들어온다 useState와 비슷하다고 보면 된다. 그리고 특이한건 ref객체를 jsx 노드의 ref 어트리뷰트로 던져주게되면 current를 해당 돔으로 설정한다. 돔자체를 참조하게된다. 📌 다음 렌더링에서 useRef는 동일한 객체를 반환한다는 사실이 중요하다.

📌 렌더링에 사용되는 애들을 조작할려면 useRef는 적합하지 않음
📌 react는 useRef가 바뀌는지 알수없기 땨문에 렌더링 안함
📌 ref.current는 렌더링 중에 쓰거나 읽지 말자
📌 ref 객체도 두 번 생성되지만, 결국 하나만 사용되므로 걱정말라 strict mode 때문임~

## 2024_09_21

### useOutletContext

React-Router
{: .label .label-yellow }

outlet에 설정된 컴포넌트에게 props를 내려주기 위한 hook이다.

```js
function Parent() {
  const [count, setCount] = React.useState(0);
  return <Outlet context={[count, setCount]} />;
}
```

```js
import { useOutletContext } from "react-router-dom";

function Child() {
  const [count, setCount] = useOutletContext();
  const increment = () => setCount((c) => c + 1);
  return <button onClick={increment}>{count}</button>;
}
```

사실 사용방법은 간단하다 context로 내려주고 이를 useOutletContext를 통해 받으면 된다.

##🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧작성해야하는 녀석들🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧

<!-- ## Hook🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

### useMemo🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

### Suspense 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴 -->
