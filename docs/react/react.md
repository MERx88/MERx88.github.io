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

### useRef🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

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

## Hook🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

### useMemo🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

### Suspense 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴
