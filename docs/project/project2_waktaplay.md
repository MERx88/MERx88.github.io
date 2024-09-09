---
layout: default
title: Waktaplay
parent: Project
nav_order: 2
---

# Waktaplay (왁타버스 뮤직플레이 어플리케이션)

요즘 우왁굳 개발팀(비영리 단체)에 합류해서 팀 프로젝트를 진행중이다. 이에 관한 일지 및 문제사항을 업로드 할 예정이다.

---

## Table of contents

- [2024_08_30](#2024_08_30)
  - [Outlet](#Outlet)
- [2024_09_07](#2024_09_07)
  - [스켈레톤에 대하여](#스켈레톤에-대하여)
  - [Suspense](#Suspense)
  - [무한 스크롤](#무한-스크롤)

---

## 2024_08_30

### 마이그레이션...하 던 중...

outlet을 프로젝트에서 쓰길래 정리했당 🤓 하면서 라우팅에 대한 공부도 다시했다.

[Outlet Link]({https://merx88.github.io/docs/Javascript/mechanism/##값의-할당}/)

## 2024_09_07

### 스켈레톤에 대하여

스켈레톤의 장ㅈ점

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

### Suspense 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴 이거 리액트로 빼야할듯?

### 무한 스크롤 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴 근데 이거 구현 안할듯

### 데이터 맛있게 불러와 보겠습니다. 근데 이제 FE 최적화를 곁들인 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

<img src="../../assets/images/Choimeme.png" width="360px">

useEffect 로 데이터를 불러오는건 당연하고... 문제는 흠 리렌더링에 대하여 인데 총 네가지 데이터가 있다.

- 실시간 탑 100
- 일간 차트
- 주간 차트
- 누적 차트

흠 페이지는 흠 우선 가장 상위 페이지인 Charts.tsx 그리고 차트 엘리먼트를 렌더링 하기 위한 ChartItem.tsx 정도 있다. (추가로 로딩을 위한 skeleton.tsx 까지)

```zsh
pages/charts
├── ChartItem.tsx
└── Charts.tsx
```

처음에는 그냥 Charts에 api 때려박고 데이터를 ChartItem 에다가 내려서 렌더링 하려고 했는데 생각해보니... 리프레쉬 버튼이 있기 때문에 실시간 정도는 빼야하지 않을까 생각했다. 근데 또 생각해보니 post 도 꽤 다 있어서 걍 다빼기로 그리고 헤더도 charts에 있었는데 이것도 뺴야겠다 체크 박스 전체선택이있어서...

```zsh
pages/charts
├── ChartDaily.tsx
├── ChartItem.tsx
├── ChartRealTime.tsx
├── ChartTotal.tsx
├── ChartWeekly.tsx
└── Charts.tsx
```

겁나 의식의 흐름으로 적었는데 그냥 get 호출은 각 차트 페이지에서 진행하는걸로... 나중에 post 호출 적용하면 바뀔지도? 우선 예상 정도 해서 파일 구조 짜놓고 다음기회에 보자...

## 2024_09_09

### 새로운 IDE 이름은 Cursor로 하겠습니다. 근데 이제 VSCode를 곁들인 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

### useEffect 데이터 호출. 근데 이제 2번 중복 호출을 곁들인 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

## 2024_09_09

### Redux -> Recoil -> 그리고 처음 보는 Zustand 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴

![zustand](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcA3Yh0%2FbtrD6yxMv3Q%2FkghmSTTbyQQ1GFIeWJn6l1%2Fimg.jpg)
