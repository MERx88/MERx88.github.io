---
layout: default
title: Waktaplay
parent: Project
nav_order: 2
---

# Waktaplay (왁타버스 뮤직플레이 어플리케이션)

![woowak z](image-3.png)

요즘 우왁굳 개발팀(비영리 단체)에 합류해서 팀 프로젝트를 진행중이다. 이에 관한 일지 및 문제사항을 업로드 할 예정이다.

---

## Table of contents

- [2024_09_07](#2024_09_07)

  - [스켈레톤에 대하여](#스켈레톤에-대하여)

- [2024_09_09](#2024_09_09)

  - [useEffect 데이터 호출. 근데 이제 2번 중복 호출을 곁들인](#useeffect-데이터-호출-근데-이제-2번-중복-호출을-곁들인)

- [2024_09_10](#2024_09_10)
  - [useState와 상태관리 라이브러리 어떤게 언제 어떻게 유리함? 그리고 나만의 기준은?](#usestate와-상태관리-라이브러리-어떤게-언제-어떻게-유리함-그리고-나만의-기준은)
  - [checkbox 선택 지멋대로 쳐대는 문제 해결](#checkbox-선택-지멋대로-쳐대는-문제-해결)
- [2024_09_11](#2024_09_11)
  - [v6.4 React Router로 동적 라우팅 해보기](#v64-react-router로-동적-라우팅-해보기)

---

## 2024_09_07

### 스켈레톤에 대하여

스켈레톤의 장점

1. 로딩시간이 비교적 짧게 느껴진다.

2. 한번에 쏟아지는 데이터를 사전에 스켈레톤을 보면서 익히면서 편안함을 느낀다.

3. 서비스가 진행 중이라는 알림 역할도 한다.

🧐 스켈레톤은 무조건 사용하는게 좋을까?

[스켈레톤에 대한 카카오 테크 블로그 링크](https://tech.kakaopay.com/post/skeleton-ui-idea/)

```md
좋은 Progress Indicator는 사용자에게 긍정적인 경험을 줄 수 있고 사용자가 작업을 끝까지 수행할 수 있도록 만들 수 있습니다.

Progress Indicator와 관련된 주요 지침은 다음과 같습니다.

1. 약 1초 이상 걸리는 작업에는 Progress Indicator를 사용하십시오.
2. Loop Animation은 빠른 동작에만 사용하십시오.
3. Percent-done Animation은 10초 이상 걸리는 작업에 사용하십시오.
4. Static Indicator는 사용하지 마십시오.

로드하는데 1초 미만이 소요되는 모든 항목의 경우 반복되는 애니메이션을 사용하면 주의가 산만해집니다. 사용자는 화면에서 어떤 일이 발생했는지 따라갈 수 없고, 화면에 깜빡이는 내용에 대해 불안을 느낄 수 있습니다.

출처: https://www.nngroup.com/articles/progress-indicators/
```

응답속도가 빠른 앱이면 오히려 스켈레톤은 걸리적 거린다. 응답속도에 따라 정해보자!

음 한 위에서 말한대로 1초 이상이면 스켈레톤과 같은 Progress Indicator 쓰자

## 2024_09_09

### useEffect 데이터 호출. 근데 이제 2번 중복 호출을 곁들인 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

{: .note }
**지연 로딩(Lazy Loading)** : 필요한 리소스나 데이터만을 필요한 시점에 불러오는 기술

## 2024_09_10

### useState와 상태관리 라이브러리 어떤게 언제 어떻게 유리함? 그리고 나만의 기준은?

{: .hilight }
🧐 zustand 사용하기 전에 갑자기 궁금한게 useState와 상태관리 라이브러리 사용 조건이다. 언제 어떻게 사용했을때 둘중에 뭐가 유리할까?

![statemanage](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRbne4NZUg4GJ6RvQ9xgEVGWS8tvBYe3BhHpQ&s)

우선 기본적으로 props driling 을 방지라는 상태관리라이브러리의 장점이 있는건 알고있다. 근데 이것만으로는 기준을 세우긴 어려워 더찾아보았다.

**useState**

state를 로컬로 관리한다.

🔵 장점

- 당연히 상태관리라이브러리 쓸때 보다 가볍다 -> 번들 크기가 줄고 성능이 올라간다.
- 조금 더 직관적인 상태관리가 가능하다고한다. -> 흠 액션같은게 빠져버리니까 조금 예측 못할수있겠다 싶다. 그리고 중앙 관리 보다 내려주는 방식이기 때문에 타입이 좁혀진다

🔴 단점

- 많은 변수가 있는 컴포넌트에서 상태를 관리하는 것은 번거롭다? -> 근데 이건 사실 상태관리라이브러리도 비슷한듯
- 당연히 props driling이 문제다 -> 그러니 depth가 깊지않다면 useState를 쓰는게 유리할지도
- 리랜더링을 유발...? -> 그러면 상태관리 라이브러리는 리랜더링 유발안하나?

**상태관리라이브러리**

🔵 장점

- props driling 없으니까 당연히 추적 댕쉽다.
- 복잡한 상태관리에 용이하다. -> 인정 비즈니스 로직에 쓰면 이득인듯
- 성능 최적화에 도움이 된다. -> 내려주는 방식이 아닌 중앙에서 뿌려주는 형식이기에 부모가 state가 바뀐다고 전부다 리렌더링 할필요가 없다.

🔴 단점

- 오히려 복잡하지않은데 쓰면 간단한 녀석이 더복잡해질수있음
- 복잡하면 디버깅이 어려울수 있음 -> 이게 아마 막 state를 여러 컴포넌트에서 쓰고 지우거나 확인 할때 어디에서 뭘했는지 파악하기가 props로 내려줄때 보다 어렵다는 소리같다.
- 협업중 누군가가 잘못건드려 버그가 생길수있다. -> 모든 컴포넌트에서 접근 가능하니 당연쓰
- 결국 모듈을 다운받고 쓰기 때문에 모듈이 업데이트 되거나 하면 번거러운 일이 생길수있다.

{: .note }
DRY : "Don't Repeat Yourself" & DX : "Developer Experience"

오케이 그러면 코드 결합성, 상태의 갯수와 복잡성, 랜더링, 컴포넌트 간의 연관성에 따라 기준을 세우자

**기준**

1. 비즈니스 로직 처럼 복잡, 이곳 저곳에서 사용(페이지 사이 정도의 거리!), 랜더링이 정말 빈번하게 일어나는 경우(게임 같은거)? -> _전역상태관리_
2. 1번의 경우를 제외한 거의 모든 경우 -> _useState_

### checkbox 선택 지멋대로 쳐대는 문제 해결

아직 모르는게 너무 많다고 느꼈다

2번, 3번 ..100번 checkbox를 선택은 쳐안되고 계속 0번 체크박스만 체크되길래 뭔가 싶었다.

checkbox ui를 고치면서 checkbox 속성들을 다시 확인했다.

[checkbox Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

id='checkboxId'로 통일이 되어있어서 다른걸 눌러도 0번만 선택되었다. 걍 개쳐멍청하네

## 2024_09_11

### v6.4 React Router로 동적 라우팅 해보기

![router]('https://global.discourse-cdn.com/business5/uploads/apollographql/optimized/2X/c/c07a70726064b8778be1f2ba6149db9c0a582795_2_1024x535.png')

라우팅에 대해 솔직히 말하자면 아주 잘 알고있다고는 못했다. 하지만 이번에 프로젝트에서 charts 부분을 맡으면서 라우팅을 제대로 해보았다. 원래 파일 구조는 이러했다.

```zsh
pages/charts
├── ChartDaily.tsx
├── ChartItem.tsx
├── ChartRealTime.tsx
├── ChartTotal.tsx
├── ChartWeekly.tsx
└── Charts.tsx
```

그리고

```js
{
  chartType === "realTime" && <ChartRealTime />;
}
{
  chartType === "daily" && <ChartDaily />;
}
{
  chartType === "weekly" && <ChartWeekly />;
}
{
  chartType === "total" && <ChartTotal />;
}
```

이렇게 페이지를 보여주었는데 바보같은 설계이다. 일단 중복 코드가 너무 많이 생긴다. 중복은 코드 작업에서 가장 멍청한 방법이다.

일단 v6.4가 무엇인지 어떻게 달라졌는지 알아보자

```xml
    <!-- v6.4 React Router -->

    <!-- index -->
    <BrowserRouter>
      <main/>
    </BrowserRouter>

    <!-- main -->
    <Routes>
      <Route path="/" element={<App/>}>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/posts">
          <Route index element={<PostList />} />
          <Route path="/post" element={<post />} />
        </Route>
      </Route>
    </Routes>

     <!-- App -->
    <Outlet>

    <!-- Nav -->
    <Link to="/about">about</Link>

```

기존에는 위와 같이 <BrowserRouter>으로 감싸주고 파일안에서 <Routes>로 <Route>를 감싸서 해당 path에 맞는 컴포넌트 를 <Link>를 누르면 보여주었다.

그리고 path를 route로 묶어 주면서 사용할 수 있었다.

```xml
    <!-- v6.4 React Router -->

    <!-- index -->
    <RouterProvider router={router} />

    <!-- App -->
    <Outlet>

    <!-- Nav -->
    <Link to="/about">about</Link>

    <!-- SomeThingPage
    const params = useParams(); -->
```

위는 달라진 사용법이다. 기존에 사용하던 <Outlet>도 보인다. 여기서 중요하게 바뀐건 props로 내려주고 있는 router 객체이다. 이게 어떤 것인지 왜 모든 Routes들은 Outlet 하나로 퉁쳐졌는지 알아보자

```js
// router.tsx

const routerConfig: RouteObject[] = [
  {
    path: "/",
    element: <Home />,
  },
  {
    path: "/about",
    element: <About />,
  },
  {
    path: "/posts",
    element: <PostList />,
    children: [
      {
        path: "/post:id",
        element: <post />,
      },
    ],
  },
];

export const router = createBrowserRouter([
  {
    path: "/",
    element: <App />,
    children: routerConfig,
  },
]);
```

router 객체는 createBrowserRouter이라는 함수를 통해 만들수 있으며 위에서 중첩으로 된 Routes 들을 위와 같이 작성할수있다. 중첨된것은 children 이라는 key에 밸류로 주어 해결가능해졌다. 그리고 나머지 key 밸류들은 기존과 똑같이 사용가능하다. 가장 상단에 <App>으로 지정되어있기 때문에 여기 있는 Outlet에 routerConfig의 모든 라우팅 값들이 빠져나오면서 <App>의 레이아웃 디자인은 유지하면서 중첩 라우팅 수행이 가능하다.

_🧐 그러면 동적라우팅은...?_

동적라우팅도 똑같다

```js
 {
    path: "/posts",
    element: <Posts />,
    children: [
      {
        path: ":id",
        element: <Post />,
      },
    ],
  },
```

요런식으로 사용하면 '/posts/[id]' 맞는 id 값으로 바뀌어서 들어올 것이고 이를 useParams 를 통해 추출하여 get Request를 활용 할 수있다.
진짜 마지막으로 <Navigate>를 통해 리다이렉션도 해줄수있다. 원하는 path 만 넣어주면 그 path로 리다이렉트 된당

아래 코드를 보면 이해가 매우 잘될수있다. 물론 내가 짠 코드라 ... 그런가?

```js
// 내가 만든 chart 페이지 일부

const { chart } = useParams();
const [data, setData] = useState([]);
const [isLoading, setIsLoading] = useState(true);
const [hasError, setHasError] = useState(false);

useEffect(() => {
  const fetchData = async () => {
    try {
      const result = await getChart(chart);
      setData(result.data.chart);
      setIsLoading(false);
    } catch (error) {
      console.error("에러 발생:", error.message);
      setHasError(true);
      return;
    }
  };
  fetchData();
}, [chart]);

if (hasError) {
  return <Navigate to="/" />;
}
```

📌 정리

- router 라는 객체에 route들을 정해놓고 이를 <Outlet>을 통해 불러올수있다. 즉, 부모에서 자식들을 <Outlet>을 통해 중첩라우팅할수있다.
- useParams 를 통해 동적라우팅된 것들(?)을 뽑아올수있다.
- <Navigate>를 통해 리다이렉션 할수있다.

그리고...

```zsh
pages/charts
├── ChartItem.tsx
├── ChartHeader.tsx
├── Chart.tsx
└── Charts.tsx
```

파일수를 확줄일수있게 되었고 중복 코드는 많이 사라졌다 👍

##2024_09_20

### ✅🤯✅🤯✅🤯✅🤯✅🤯 checkBox 전체선택 구현하기~ 🤯✅🤯✅🤯✅🤯✅🤯✅

우선 배열로 체크박스 관리하면 될듯

배열 요소 확인해서 체크박스 요소에서 하나라도 빠지면 전체해제

근데 Outlet에 어떻게 props를 내리지...했는데 useOutletContext가 있었다

[useOutletContext Link](https://tech.kakaopay.com/post/skeleton-ui-idea/)

근데 charts.tsx가 아닌 chart.tsx 에서 부터 props를 내려주면 되어서 그냥 안쓰기로 했다. 하하...(파일 구조는 다음과 같다.)

```zsh
src/renderer/pages/charts
    #각 주기별 차트
├── Chart.tsx
    #차트 찐 내용물의 헤더 녀석
├── ChartHeader.tsx
    #차트 찐 내용물의 아이템 엘리먼트
├── ChartItem.tsx
    #차트 페이지
└── Charts.tsx
```

아까도 말했듯이 체크박스로 선택된 녀석들의 아이디를 배열로 저장하고 요소의 갯수에 따라서 전체 선택도 하고 해제도 하고 하면 된다고 생각했다.

우선 이기능이 왜 있느냐

![actionrow]('docs/project/actionRow.png')

체크박스 선택하면 셔플링 재생 등등 actionrow를 조작하기 위해 체크박스 기능을 구현해야한다.

- ui로 몇곡 선택되었는지 보여줘야한다.
- 그리고 재생이나 이런 처리를 서버에게 보내주어야한다. 근데 아직 이 처리는 안하기 때문에 우선 염두해두고 개발해야한다.

배열로 구현할거기 때문에 우선 state를 배열로 진행하고 이 길이를 ui로 보내주면 된다. 그리고 state 배열로 모아둔 아이디들을 서버에 보낼때 사용하면 될거 같다. 뭐 우선 이정도 생각하고 체크박스 구현을 본격적으로 시작해보자

여러 케이스가 있다. 일단 크게 두가지 케이스는 전체선택 체크박스, 개별선택 체크박스 두가지 케이스로 나눌 수있다. 그리고 간접조작이랑 직접조작 두가지로 나눌 수도 있다. (간접조작은 개별선택과 전체선택이 서로 영향을 미치는 경우를 말한다.)

전체선택 체크박스

- 직접조작 (개별선택 간접과 동일)

  - 전체선택 true -> 개별선택 100개 모두 true -> state에 모든 아이템 추가 -> 총 100개
  - 전체선택 false -> 개별선택 100개 모두 false -> state에 모든 아이템 제거 -> 0개로 초기화

- 간접조작

  - 개별선택 100개중 1개 이상 false -> 전체선택 false -> state에 해당 개별 선택 제거
  - 개별선택 모두 100개 true -> 전체선택 true -> state에 100개 모두 들어있어야함

개별선택 체크박스

- 직접조작

  - 개별선택 1개 true -> state에 해당 아이템 추가
  - 개별선택 1개 false -> state에 해당 아이템 삭제

- 간접조작 (전체선택 직접과 동일)

  - 전체선택 true -> 개별선택 100개 모두 true -> state에 모든 아이템 추가 -> 총 100개
  - 전체선택 false -> 개별선택 100개 모두 false -> state에 모든 아이템 제거 -> 0개로 초기화

우선 위의 조건들을 만족하게 함수를 짜야한다. 껄껄

사실 내가 checkbox ui를 잘못 만들어서 그냥 잘못 만들어진대로 useEffect를 써서 만들려고 했지만 isChecked라는 state와 배열 state가 변할때 마다 리렌더링으로 useEffect로 할려고 했지만 state끼리 꼬이는 문제가 생기고 가장 큰 문제는 가독성이었다. 어쩔수없이 그냥 ui 를 고치기로 하고 다시 함수를 만들어 보았다. 아 그리고 useRef로 해보려고 했는데 아직 숙련도가 높지 않아서 어렵기도 하고 이를 ui 에 반영하려면 또 state에 담아야 리렌더링으로 ui가 업데이트 된다. 그리고 해보다가 안 사실인데 useRef를 useEffect 의존성 배열에 넣어도 이로인해 useEffect가 다시 실행되지 않는것을 확인 할수있었다. 물론 이제는 useEffect를 사용해서 전적으로 체크박스를 조작하지는 않을거지만 우선 이렇게 한번 시행착오를 겪었다라는 것을 남기고 싶었다.

사실 이제부터 진짜 구현이다.

내 chart 컴포넌트는 두개의 chartItem 과 chartHeader 가 있다. chartItem 은 당연히 map으로 응답 받아온 데이터를 뿌려주고 있다. 다음과 같은 구조를 가지고 있다.

```js
//Chart.tsx
<Container>
  <ChartHeader />
  {data.map((song, index) => (
    <ChartItem />
  ))}
</Container>
```

우리는 앞서서 header와 아이템이 서로 어떻게 영향을 미친다는 것을 알수있었고 이를 구현하려면 아이디를 관리하는 데이터셋 state를 가장 상단에서 불러와서 header와 item 들에게 내려주면서 데이터셋을 업데이트 해야한다고 생각했다. 그리고 actionRows에 몇개가 선택되었는지 보여주어야하기 때문에 해당 컴포넌트에서 불러오면 최적이라고 생각했다.

그리고 좀 중요한건데 계속 배열로 진행하려고 했는데 배열은 중복을 허용하는 특성이 있어서 Set을 사용해서 중복을 없애기로 했다. 그리고 이를 결국 스프레드로 배열에 풀면 배열의 특성도 이용할수있기 때문에 중복 금지를 우선 조건으로 Set으로 진행했다.

```js
//Chart.tsx
const [checkedItems, setCheckedItems] = useState<Set<string>>(new Set())

<Container>
  <ChartHeader checkedItems={checkedItems} setCheckedItems={setCheckedItems}/>
  {data.map((song, index) => (
    <ChartItem
      checkedItems={checkedItems}
      setCheckedItems={setCheckedItems}
    />
  ))}
  <ActionRows checkedItems={checkedItems} />
</Container>
```

우선 개별선택부터 구현해보았다. 우선 직접 조작은 다음과 같았다.

```md
- 직접조작

  1. 개별선택 1개 true -> state에 해당 아이템 추가
  2. 개별선택 1개 false -> state에 해당 아이템 삭제
```

그렇다면 input의 type을 checkbox로 설정하고 해당 체크박스가 체크 유무가 바뀔때마다 값을 확인하고 checkedItems에 해당 id를 추가 하기로했다. 이렇게 1번 직접조작을 구현할수있고 2번은 1번이 아닌경우 즉, 체크가 안된경우 해당 id를 checkedItems에서 제거 하면된다. 이걸 코드로 그대로 구현하면 다음과 같이 된다.

중요한 사실 이때 사실 event.target.checked로 값을 가져올수있다 하지만 앞으로 해당 dom을 참조해서 사용해야할일이 한번 더 남았으므로 useRef를 통해 dom을 참조하기로했다. 통일성도 있고 어짜피 ref를 써야만 하는 상황이고 참조 하면 메모리 먹고 있을텐데 말이다.

```js
//ChartItem.tsx
const checkBoxRef = useRef(null);

//직접 조작
function handleCheckbox() {
  if (checkBoxRef.current.checked) {
    setCheckedItems((prev) => new Set(prev).add(song.id));
  } else {
    setCheckedItems((prev) => {
      const newSet = new Set(prev);
      newSet.delete(song.id);
      return newSet;
    });
  }
}

<input
  type="checkbox"
  id={song.id}
  name="song"
  ref={checkBoxRef}
  value={song.id}
  onChange={handleCheckbox}
/>;
```

조금은 덜 직관적인 간접 조작은 다음과 같았다.

```md
- 간접조작 (전체선택 직접과 동일)

  1. 전체선택 true -> 개별선택 100개 모두 true -> state에 모든 아이템 추가 -> 총 100개
  2. 전체선택 false -> 개별선택 100개 모두 false -> state에 모든 아이템 제거 -> 0개로 초기화
```

만약 전체선택에서 체크박스를 선택하면 위와 같은 일이 일어나고 개별선택에서는 이에 반응해야하기에 useEffect로 반응을 감지하고 진행하는게 맞을것이다. 사실 간단하다 checkedItems를 의존성 배열에 넣고 이가 바뀔때마다 내가 포함되는지 확인하면된다 포함되면 ref로 참조해둔 checkBox 값을 스리슬쩍 체크로 바꾸면된다.

```js
//ChartItem.tsx
const checkBoxRef = useRef(null)

//직접 조작
function handleCheckbox() {
  if (checkBoxRef.current.checked) {
    setCheckedItems(prev => new Set(prev).add(song.id))
  } else {
    setCheckedItems(prev => {
      const newSet = new Set(prev)
      newSet.delete(song.id)
      return newSet
    })
  }
}

//간접 조작
useEffect(() => {
  checkBoxRef.current.checked = checkedItems.has(song.id)
}, [checkedItems])


<input type="checkbox" id={song.id} name="song" ref={checkBoxRef} value={song.id} onChange={handleCheckbox} />
```

개별선택은 완료되었다 👏👏

전체선택도 흐름은 비슷하다 빠르게 가보자 🏃

```md
- 직접조작 (개별선택 간접과 동일)

  1. 전체선택 true -> 개별선택 100개 모두 true -> state에 모든 아이템 추가 -> 총 100개
  2. 전체선택 false -> 개별선택 100개 모두 false -> state에 모든 아이템 제거 -> 0개로 초기화
```

개별조작처럼 선택되면 onChange로 확인하고 api로 받아온 데이터의 모든 id를 checkedItems에 추가하면 된다. 당연히 체크 해제되면 다 지우면 된다.

=> 그러면 아까 설정해둔 개별 선택 useEffect가 반응해서 자기 아이디가 포함되어있는지 확인하고 있다면 체크가 될것이다!

```md
- 간접조작

  - 개별선택 100개중 1개 이상 false -> 전체선택 false -> state에 해당 개별 선택 제거
  - 개별선택 모두 100개 true -> 전체선택 true -> state에 100개 모두 들어있어야함
```

간접조작은 100개의 데이터가 체크가 되어있다면 전체선택 체크박스돠 체크가 되어야한다. 물론 99개만 되어도 해제되어야한다. 이것도 useEffect로 checkedItems을 확인하고 사이즈를 체크한후 ref로 참조되어있는 전체선택 체크박스를 스리슬쩍 바꾸면 된다.

```js
const allCheckBoxRef = useRef(null)

function handleAllCheckbox() {
  if (allCheckBoxRef.current.checked && data) {
    setCheckedItems(new Set(data.map(el => el.id)))
  } else {
    setCheckedItems(new Set())
  }
}

useEffect(() => {
  allCheckBoxRef.current.checked = checkedItems.size >= 100
  }, [checkedItems])

<input
  type="checkbox"
  id="allCheckBox"
  name="song"
  value="allCheckBox"
  ref={allCheckBoxRef}
  onChange={handleAllCheckbox}
/>
```

👏👏👏👏👏👏 이렇게 모든 체크박스 완료 👏👏👏👏👏👏

사실 처음에는 살짝 막막하고 오기 부리다가 삽질을 쬐금했는데 이런저런 기능을 써볼수있는 feature여서 나의 fe 지식이 조금은 더 확장 된거같은 기분,,,

아래는 새로 알게된 개념들을 정리했다, checkbox도 이런저런 기능을 알게 되었고 무엇보다 useRef에 대해 알게 되었다.

[useRef Link](https://tech.kakaopay.com/post/skeleton-ui-idea/)
[checkbox Link](https://tech.kakaopay.com/post/skeleton-ui-idea/)

### ✅ checkBox 컴포넌트 설계하기

체크박스 컴포넌트 재사용성을 생각하며 다시설계하다가 새로 알게 된 사실들과 개선된 체크박스 설계를 어떻게 했는지 적어본다

전체선택을 구현하다가 나의 체크박스 설계가 잘못되었다는 것을 알고 기존 코드를 수정하게 되었다. 정확하게는 input checkbox에 대한 이해가 부족해서 온전하게 체크박스의 기능을 사용하지 못해 확장성, 재사용성이 떨어지는 컴포넌트였다.

**기존 코드**

_styled components로 작성된 css는 생략했다._

```jsx
import React from "react";
import styled from "styled-components";
import CheckboxChecked from "@assets/icons/checkbox_filled.svg";
import CheckboxUnchecked from "@assets/icons/checkbox_unfilled.svg";

const CheckBox = ({
  id,
  name,
  value,
  text,
  isChecked = false,
  setIsChecked,
}: {
  id: string,
  name?: string,
  value?: string,
  text?: string,
  isChecked: boolean,
  setIsChecked: React.Dispatch<React.SetStateAction<boolean>>,
}) => {
  return (
    <Container htmlFor={id} text={text}>
      <HiddenCheckbox
        type="checkbox"
        id={id}
        name={name}
        value={value}
        checked={isChecked}
        onChange={() => {
          setIsChecked(!isChecked);
        }}
      />
      <img src={isChecked ? CheckboxChecked : CheckboxUnchecked} />
      {text ? <Text>{text}</Text> : null}
    </Container>
  );
};

export default CheckBox;
```

체크박스 전체선택을 구현하면서 맞닥뜨린 문제는 우선 두가지였다.

- react hook인 useRef를 통한 ref를 사용못하는 것 -> 유용한 ref를 사용하지못해 다른방법으로 Dom에 접근해야한다는 것
- onChange를 사용하지 못하는 것 -> 체크박스 체크만 가능하고 다른 이벤트는 일으킬수 없는것

기존 코드는 onChange를 check 만을 컨트롤 하고 있었다. 그리고 부모 컴포넌트에서 useState를 하나 선언한뒤 그저 true 와 false를 반환하고 ui를 그에 맞게 렌더링 하고 있을 뿐이었다.

**ref 받아오기**

ref를 받아오는 것은 어렵지 않았다. 부모에서 받아오는 ref를 <HiddenCheckbox>에 잘 넘겨주기만 한다면 된다. 근데 이때 forwardRef를 통해 컴포넌트를 감싸주어야한다.

**onChange 받아오기**

onChange를 받아오는 과정에서 그냥 onChange를 받아서 내려주다가 state를 어떻게 바꿔주지 라는 생각이 들었다. 그러면 우선 onChange를 onChange에 넣어주자 setiseChecked를 넣어주었던거 처럼!

```js
return (
  <Container htmlFor={id} text={text}>
    <HiddenCheckbox
      type="checkbox"
      id={id}
      name={name}
      value={value}
      checked={isChecked}
      onChange={(e) => {
        onChange(e);
        setIsChecked(!isChecked);
      }}
    />
    <img src={isChecked ? CheckboxChecked : CheckboxUnchecked} />
    {text ? <Text>{text}</Text> : null}
  </Container>
);
```

하지만 이는 부모에서 꼭 onChange를 내려주어야만 작동했다. 왜냐하면

##🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧작성해야하는 녀석들🚧🚧🚧🚧🚧🚧🚧🚧🚧🚧

<!-- ### 무한 스크롤 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴 근데 이거 구현 안할듯

### checkbox 다중 선택 만들기

### hook vs util 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

{: .hilight }
🧐 중복되는 로직을 빼놓는건 당연한 개발자의 숙명이다. 근데 보통 utils, hooks 파일 두가지가 있는데 어떤 기준으로 뺼까?

### Redux -> Recoil -> 그리고 처음 보는 Zustand 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

![zustand](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcA3Yh0%2FbtrD6yxMv3Q%2FkghmSTTbyQQ1GFIeWJn6l1%2Fimg.jpg)

와 모르던 사실 리코일 번들 사이즈 왤캐 크냐 23.5kb네... zustand 익숙해지면 zustand 만 써야겠당 1.1kb 많이 작다. -->

```

```
