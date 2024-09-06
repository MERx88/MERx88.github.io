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

### Outlet 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴 이거 리액트로 빼야할듯?

## 2024_09_07

### 스켈레톤에 대하여

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

### 무한 스크롤 🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴🔴
