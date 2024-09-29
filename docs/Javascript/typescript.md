---
layout: default
title: Typescript
parent: Javascript
nav_order: 6
---

# Typescript

![typescript](image-1.png)

자바스크립트의 수퍼셋 타입스크립트 타입이 있어서 더 좋은거라고...? 맞긴한데 타입스크립트는 C보다도 더러운 느낌이 든다. 그냥 그렇다구

## 2024_09_19

### `// @ts-ignore`

컴파일러에게 다음 줄의 코드에 대한 타입 검사를 무시하도록 지시하는 주석

{: .note }
당연히 남용하면 타입스크립트 사용하는 의미가 없어진다.

## 2024_09_28

### 🚧🚧 Enum 🚧🚧

🚧 ...작성중... 🚧
{: .label .label-yellow }

내가 chart를 만들고 pr을 날렸는데 팀장님이 enum 타입을 써서 string으로 되어있던 chart 타입을 좀더 좁혀주는게 좋겠다고 리뷰를 해줬다. 그래서 뭔지 찾아보았다.

어떤 값이 들어오는지 어느정도 정해져있을때 값의 종류를 나열하여 그 값의 종류로 타입을 제한하는 것이다. 말이 어려우니 한번 보자

```ts
export async function getChart(chart: string) {
  const response = await fetch(`https://api/${chart}`);
  const body = await response.json();
  return body;
}
```

기존 코드다 chart의 타입이 string으로 어떤 string 값이든 파라미터로 받을 수 있다. 근데 해당 프로젝트의 chart string 값은 단 네가지 이다. "realtime" | "weekly" | "daily" | "total" 그렇기 때문에 이 네가지만 받을수 있도록 타입을 좁혀주는 것이 좋다.

enum을 사용하면 아래와 같이 타입을 좁힐수있다.

```ts
enum EChartType {
  REALTIME = "realtime",
  WEEKLY = "weekly",
  DAILY = "daily",
  TOTAL = "total",
}

export async function getChart(chart: EChartType) {
  const response = await fetch(`https://api/${chart}`);
  const body = await response.json();
  return body;
}
```

chart에 값이 들어오고 이 값을 enum의 EChartType을 통해 검사하게되고 "realtime" | "weekly" | "daily" | "total" 중 있으면 정상적으로 함수를 실행시킨다.

enum은 위와 같이 값을 지정안하면 0부터 차례로 값을 매긴다.

```ts
enum Day {
  Day1, // 0
  Day2, // 1
  Day3, // 2
}
```

그러면 사실 `const day : Day` 라고 선언하면 0,1,2가 들어올수도 있고 Day.Day1, Day.Day2, Day.Day3 도 들어올수있다. 이렇게 되면 예기치 못한 문제가 생길수 있기 때문에 값은 처음 봤던거 처럼 지정해두고 쓰는 것이 가장 올바른 사용방법이다. (0은 false로도 인식 되기 때문에 문제가 생길 수있다.)

{: .highlight-title }

> 🚧 Not finished yet

> 우선은 이 정도로 정리하지만 앞으로 더 추가 될수도 있다. tree shaking 할 때 Enum이 안좋다는 말이 있어서...
