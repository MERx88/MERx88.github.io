---
layout: default
title: Waktaplay
parent: Project
nav_order: 2
---

# Waktaplay (왁타버스 뮤직플레이 어플리케이션)

![wz]('https://cafe.naver.com/common/storyphoto/viewer.html?src=https%3A%2F%2Fcafeptthumb-phinf.pstatic.net%2FMjAyNDA5MDdfMTMz%2FMDAxNzI1NjUwMjYyOTQx.BPJ1q6LxYjHabOeNsvxy_zjtAlnFFe8E-i-Qrzma0Owg.YUhowYtNo60EgNI6hQv_gsz-zPAbumWhSWxQYkU_wMEg.PNG%2F%25EC%259A%25B0%25EC%2599%2581%25EA%25B5%25B3Z-%25EC%25B1%2584%25EB%2584%2590%25EC%2595%2584%25ED%258A%25B8.png%3Ftype%3Dw1600')

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

---

## 작성해야하는 녀석들

<!-- ### 무한 스크롤 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴 근데 이거 구현 안할듯

### checkbox 다중 선택 만들기

### hook vs util 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

{: .hilight }
🧐 중복되는 로직을 빼놓는건 당연한 개발자의 숙명이다. 근데 보통 utils, hooks 파일 두가지가 있는데 어떤 기준으로 뺼까?

### Redux -> Recoil -> 그리고 처음 보는 Zustand 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

![zustand](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcA3Yh0%2FbtrD6yxMv3Q%2FkghmSTTbyQQ1GFIeWJn6l1%2Fimg.jpg)

와 모르던 사실 리코일 번들 사이즈 왤캐 크냐 23.5kb네... zustand 익숙해지면 zustand 만 써야겠당 1.1kb 많이 작다. -->
