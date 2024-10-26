---
layout: default
title: 📦 npm
parent: React
nav_order: 1
---

## 🚧🚧 npm 🚧🚧

node.js 패키지 관리인 npm!

### 🚧🚧 package.json 과 package-lock.json 🚧🚧

우테코 공통 피드백을 보다가 흠 나 이 두개 완벽히 이해하고 있나? 그냥 패키지 관리해주는 고마운 친구정도로만 알고잇는거 아닌가? 해서 정리하게 되었다.

> ### package-lock.json의 역할을 이해한다
>
> package.json 파일은 일반적으로 유의적 버전(semantic versioning)을 사용하며, package-lock.json에는 파일이 생성될 당시의 의존성 트리에 대한 정보가 있다. 이를 통해 node_modules를 커밋하지 않더라도 팀원들이 동일한 의존성을 설치할 수 있게 한다.

간단하게 우테코 프리코스 2주차 자동차 경주 과제를 보며 이해해보자

```json
//package.json

{
  "name": "javascript-racingcar",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "start": "node src/index.js",
    "test": "jest --detectOpenHandles"
  },
  "devDependencies": {
    "@babel/core": "^7.25.8",
    "@babel/preset-env": "^7.25.8",
    "babel-jest": "^29.6.0",
    "jest": "^29.6.0"
  },
  "dependencies": {
    "@woowacourse/mission-utils": "^2.2.0"
  },
  "jest": {
    "transform": {
      "\\.js$": "babel-jest"
    }
  },
  "babel": {
    "presets": ["@babel/preset-env"]
  },
  "engines": {
    "npm": ">=10.8.2",
    "node": ">=20.17.0"
  }
}
```

package.json 간단하다!

```json
{
  "name": "javascript-racingcar",
  "version": "0.0.0",
  "lockfileVersion": 3,
  "requires": true,
  "packages": {
    "": {
      "name": "javascript-racingcar",
      "version": "0.0.0",
      "dependencies": {
        "@woowacourse/mission-utils": "^2.2.0"
      },
      "devDependencies": {
        "@babel/core": "^7.25.8",
        "@babel/preset-env": "^7.25.8",
        "babel-jest": "^29.6.0",
        "jest": "^29.6.0"
      },
      "engines": {
        "node": ">=20.17.0",
        "npm": ">=10.8.2"
      }
    },
    "node_modules/@ampproject/remapping": {
      "version": "2.3.0",
      "resolved": "https://registry.npmjs.org/@ampproject/remapping/-/remapping-2.3.0.tgz",
      "integrity": "sha512-30iZtAPgz+LTIYoeivqYo853f02jBYSd5uGnGpkFV0M3xOt9aN73erkgYAmZU43x4VfqcnLxW9Kpg3R5LC4YYw==",
      "dev": true,
      "license": "Apache-2.0",
      "dependencies": {
        "@jridgewell/gen-mapping": "^0.3.5",
        "@jridgewell/trace-mapping": "^0.3.24"
      },
      "engines": {
        "node": ">=6.0.0"
      }
    }
    //..무려 6808줄이다.ㅋㅋㅋ
  }
}
```

개많다... 둘다 패키지 관리해주는거 같은데 왤캐 차이가 날까?

package.json은 패키지 버전 범위를 저장한다.

package-lock.json은 패키지의 정확한 버전을 저장한다.

간단하게 말하면 버전범위를 저장하는 package.json의 부족한 부분을 package-lock.json가 정확하게 버전을 알려줌으로서 도와준다고 할수있다.

그래서 내가 깃헙에서 다른 사람이 한 파일들을 clone하거나 pull한후 npm install을 하면 clone 이나 pull 할 때 받은 package-lock.json에 있는 버전들과 정확히 똑같은 패키지들을 받을수있는것이다.

말그대로 버전들을 스트릭트하게 lock을 걸어주는거라고 볼수잇다.

![package.json](image-3.png)

🤔 그럼 왜 따로 관리할까?

1. 귀찮니즘
   아까도 보았지만 한 패키지에도 엄청나게 많은 dependencies가 깔리는것을 볼수있다. 패키지 개발자가 패키지를 업데이트 했을때마다 맞춰서 버전을 수정한다면 버전 관리는 힘이 번거로울이다.

2. 가독성
   생각해보면 이렇게 나눠서 관리하면 굉장히 가독성이 좋아진다. 내부의 의존성까지 확인하지 않고 가능 큰틀에서 어떤 패키지가 있는지만 보면 되기 때문이다.
