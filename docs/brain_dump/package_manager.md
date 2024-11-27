---
layout: default
title: 👨‍🏭 package manager
parent: Brain DUUMP!
nav_order: 3
---

# 👨‍🏭 package manager

npmpnpmyarn...

## npm vs yarn

노드 모듈 관리

### npm

- 순차적 처리 -> 느림
- 패키지에 포함한 다른 패키지도 설치 -> 보안 안좋음

### yarn

- 병렬적처리 -> 빠름
- 에러가 덜남
- 명령어가 짧음
- yarn.lock, package.json에 있는 파일만 설치 -> 보안 좋음

### 그래서 뭐 써야해?

npm 이 업데이트하면서 보안 속도 측면 yarn 만큼 좋아짐 -> 취향 차이임

{ .note }

> 프로젝트 하나에 하나의 패키지 매니징 도구만 쓰자
