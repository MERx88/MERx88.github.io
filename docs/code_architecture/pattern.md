---
layout: default
title: 🔳 Pattern
parent: Code Architecture
nav_order: 2
---

# 🔳 패턴

패턴들에 대해 아라보자!

**📖 디자인 패턴이란?**

프로그램 개발에서 빈번하게 나타나는 과제를 해결하기 위한 방법

## 🕹️ MVC 패턴

![mvc](image-2.png)

우선 전체적으로 한번 있는 docs와 영상들을 읽고 보면서 느낀점? 배운점?은 내가 지금 프론트엔드 개발자면서 이런 기초적인 패턴도 모르고 공부했나 싶었다.

어떻게 보면 웹 프로그래밍이 프론트엔드 백엔드로 나뉠수 있게 도와준 패턴인데 말이다.

이를 역설적으로 말하면 이미 내가 알고 있는 패턴이었다. 추상적으로 알고 있는 이것을 구체화 시켜보자

### 가장 기본적인 설명

사실 MVC 패턴 보면서 가장 좀 빡친게 비슷하면서도 다다르다는 것이었다. 그러다가 영상을 찾아보면서 나만 이렇게 느낀게 아니란걸 알수 있었다. 그래서 다른 설명을 빼고 가장 본질적인것만 정리했다.

위에 나온 그림은 사실 더 구체화하고 웹에서 어떻게 쓰일수 있는 지에 대한 내용을 담은 그림이고

아래 그림이 제일 베이스한 그림이라고 생각한다.

![mvc2](image-3.png)

결국 세가지 파트로 나누어서 프로그램을 관리한다는 것이다. 세가지 파트는 다음과 같다

- 모델: 데이터와 비즈니스 로직을 관리합니다.
- 뷰: 레이아웃과 화면을 처리합니다.
- 컨트롤러: 모델과 뷰로 명령을 전달합니다.

더 쉬운 말로 해보면

모델 : 데이터 저장
뷰 : UI 화면 보여주기
컨트롤러 : 모델 뷰를 이어주면서 로직처리하기

하지만 사람들이 개발을 하다보면 세가지 파트 중에 포함하기 애매한것들도 생겨나게 된다. 특히 컨트롤러는 이것저것 다하는데 이걸 더 분리하는 경우도 있고 모델이나 뷰를 더쪼개는 경우도 있다. 사실 이래서 많은 사람들 정리글을 보면 다른 것이다.

[MDN MVC패턴 링크](https://developer.mozilla.org/ko/docs/Glossary/MVC)

**왜 생겨났을까?**

문제는 많지만 단하나만 뽑으라고 하면

`유지보수` 이다.

유지보수가 좋다는 건 여러방면에서 좋을 수 있지만 이것도 단하나만 뽑으라고 하면

`관심사 분리` 이다.

내가 사용자 인터페이스에 집중하고 싶으면 뷰만 보면 되고 기존 데이터 저장 방식과 데이터를 바꾸고 싶다면 모델만 확인하면 된다. 이러한 분리가 지금의 프론트엔드 백엔드 프로그래머가 만들어지고 서로의 코드하나모르더라도 API만 주고 받으면 애플리케이션이 만들어지는 것이다.

`유지보수` `관심사 분리` 이 두개의 핵심만 안다면 코드를 작성하는것도 어떤 장점이 있는지도 파생되어서 나올 수있다.(내가 프론트엔드 개발자 여서 바로 생각할수있는거 같기도 하다)

근데 Trade off가 있는거 아냐? 할수도 있는데 물론 있다. 그래서 다양한 해결법이 또 등장하는데 단점은 다른 패턴이 나올때 뭐가 문제여서 나왔는지 보면서 익히면 좋을거 같다.

**작성하는 법**

오케이 뷰 모델 컨트롤러 세가지를 나눠서 작성하면 된다고? 알았어! 하면서 짜다 보면 애매하게 판단이 흐려지는 경우가 생긴다 다른 사람들의 판단 기준을 일단 참고해서 작성해보고 나만의 판단 기준은 여기에 나중에 추가해보려 한다

[누군가의 기준 1](https://mundol-colynn.tistory.com/147)

1. 각 구성 요소의 역할과 책임을 명확하게 구분
2. 구성 요소간의 결합도 최소화
3. 코드의 재사용성과 확장성 고려

[누군가의 기준 2](https://m.blog.naver.com/jhc9639/220967034588)

모델

- 사용자가 편집하길 원하는 모든 데이터를 가지고 있어야 한다.
- 뷰나 컨트롤러에 대해서 어떤 정보도 알지 말아야 한다
- 변경이 일어나면, 변경 통지에 대한 처리방법을 구현해야만 한다.

뷰

- 모델이 가지고 있는 정보를 따로 저장해서는 안된다.
- 모델이나 컨트롤러와 같이 다른 구성요소들을 몰라야 된다.
- 변경이 일어나면 변경통지에 대한 처리방법을 구현해야만 한다.

컨트롤러

- 모델이나 뷰에 대해서 알고 있어야 한다.
- 모델이나 뷰의 변경을 모니터링 해야 한다.

[누군가의 기준 3](https://www.youtube.com/watch?v=ogaXW6KPc8I&t=397s)

1. 모델은 컨트롤러나 뷰에 의존하면 안된다.
   모델 내부에 컨트롤러 및 뷰와 관련된 코드가 있으면 안된다.
2. 뷰는 모델에만 의존해야 하고, 컨트롤러에는 의존하면 안된다.
   뷰 내부에 모델의 코드만 있을 수 있고, 컨트롤러의 코드가 있으면 안된다.
3. 뷰가 모델로부터 데이터를 받을 때는 사용자마다 다르게 보여주어야 하는 데이터에 한해서만 받아야 한다.
4. 컨트롤러는 모델과 뷰에 의존해도 된다.
   컨트롤러 내부에는 모델과 뷰의 코드가 있을 수 있다.
5. 뷰가 모델로부터 데이터를 받을 때는 반드시 컨트롤러에서 받아야 한다.

## 🦹‍♀️ 프록시 패턴

{ .note }
해당 [inpa Dev 프록시 패턴](https://inpa.tistory.com/entry/)[Refactoring guru 프록시 패턴](https://refactoring.guru/ko/design-patterns/proxy) 링크를 참고하여 작성되었습니다

![alt text](image-5.png)

프록시 대리인이라는 뜻이다. 무언가 일을 대리로 해준다는 뜻인데 프로그래밍에서 어떻게 사용될까 지금 부터 살펴보자

![alt text](image-1.png)

위 그림을 보면 사용자는 객체를 직접적으로 DoAction을 하는 것이 아닌 프록시를 한번 거쳐서 객체에 접근하는 모습을 확인 할수있다.

![alt text](image-4.png)

어떤 메소드를 실행할때 프록시 메서드에 접근한뒤 한번 로직을 거쳐서 객체에 접근해서 메소드를 실행 한다.

> 프록시는 원본객체와 같은 메서드를 구현하고 있다. 인터페이스를 통해 이작업을 할수있다.

🧐 그렇다면 바로 그냥 실행하면 되지 왜 프록시를 껴서 리소스를 낭비하는 것일까?

그 이유는 대상 클래스 즉, 객체가 민감한 정보를 들고 있거나 인스턴스화 하기에 무겁거나 원본 객체를 수정할수 없는 상황일때를 해결하고자 함이다.(이러한 문제들에 따라 보호 프록시, 가상 프록시 등 다양한 종류의 프록시 패턴이 있다.)

[오픈제플린 프록시](https://blog.openzeppelin.com/proxy-patterns)

그래서 블록체인 스마트 컨트랙트 같은 경우도 프록시 패턴을 통해 컨트랙트를 업데이트 하고자 하는 시도를 볼수있다.

### 장점

- 개방 폐쇄 원칙(OCP) 준수

- 단일 책임 원칙(SRP) 준수

- 원래 하려던 기능을 수행하며 그외의 부가적인 작업(로깅, 인증, 네트워크 통신 등)을 수행하는데 유용하다.

- 클라이언트는 객체를 신경쓰지 않고, 서비스 객체를 제어하거나 생명 주기를 관리할 수 있다.

- 사용자 입장에서는 프록시 객체나 실제 객체나 사용법은 유사하므로 사용성에 문제 되지 않는다.

### 단점

- 많은 프록시 클래스를 도입해야 하므로 코드의 복잡도가 증가한다.

- 프록시 클래스 자체에 들어가는 자원이 많다면 서비스로부터의 응답이 늦어질 수 있다.

### 요약

프록시 패턴은 중간에 프록시라고하는 대리자를 만들어서 한번 다양한 로직들을 한번 거친후 원본 객체의 메서드를 실행할수있게 만든 패턴이라고 보면 된다
