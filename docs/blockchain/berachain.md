---
layout: default
title: 🐻⛓️ berachain
parent: Blockchain
nav_order: 8
---

# berachain

프로젝트로 우연히 베라체인하게 되어서 곰돌이 계속 보는데 토할거같다 그래도 정리해보자

## PoL

사실 베라체인은 PoL을 안다면 다아는거다. 이게 핵심이자 끝이다.(사실 비콘키트도 있는데 나중에 공부 좀 더하면 다뤄보겠다.)

Proof of Liquidity

유동성 증명이라는 이야기 이다. 지금 현존하는 합의 기술은 많지만 간단하게 딱 쪼개면 PoW와 PoS이다 물론 더 많지만 대표적인 합의방식은 이 두가지 이다. 사실 PoW는 합의?라는 어감보다 강제 합의 같긴한데 뭐 여튼 두가지가 있다.

근데 늘 새로운 기술이 나온다면 문제점이 있기에 나오는 것이고 항상 TradeOff가 존재한다. PoW가 환경을 파괴 시키고, 탈중앙을 위협하고 등등 문제가 생겨 PoS가 등장했고 해당 PoS가 문제가 있어 PoL이 등장 한것이다. 그럼 무슨 문제가 있을까?

## PoS의 문제점과 그의 대안 PoL?

[Flow of Value: Examining the differences between PoS and PoL - a case for a new paradigm in sustainable incentive alignment at the protocol layer](https://blog.berachain.com/blog/flow-of-value-examining-the-differences-between-pos-and-pol-a-case-for-a-new-paradigm-in-sustainable-incentive-alignment-at-the-protocol-layer)

이 글에 PoL의 필요성에 대해 아주 잘나와있다 그중에서 중요한 문단은 다음과 같다.

`Because of the inherent risk presented to validators, they earn a bulk of the rewards that come from being selected to validate blocks. Users, on the other hand, are entirely separate from this chain of command, unable to receive proper reward distribution from the protocol level. Even further, protocols and validators within PoS Ethereum are far from aligned, with protocols unable to improve security and validators separated from the benefits provided by protocols.

Within Ethereum’s PoS model, there is no collaboration between protocols and the validator set, as there simply isn’t a need to align towards a central goal when incentives for validators and protocols are entirely different and detached from each other. Protocols are probably less concerned with the economic security of the chain they’re deployed on than validators are, just as validators are less concerned with the protocols driving activity as long as it proves valuable to them - this is a growing issue that needs to be addressed. There can't be significant collaboration amongst a decentralized set of individuals without communication, something needs to change.`

요약하면 프로토콜, 검증자(validator), 유저 새 주체가 따로 논다는 것이다. 서로 알빠냐 하면서 각자의 이득을 향해 달려가고 이는 전체 그림에서 문제가 생길수있다는 말이다.

그렇다면 서로가 하는 행위들이 영향을 미치고 서로가 이득(인센티브)을 얻는데 영향을 미친다면 생태계가 더 좋은 방향으로 나아갈수있다라고 생각했고 이러한 생각을 기반으로 PoL이 나오게 된것이다.

## 그럼 어떻게 서로가 영향을 긍정적으로 영향을 미치는 생태계를 만들건데?

그럼 PoS의 어떤 부분부터 뜯어 고쳐야할까? (앞으로 이더리움과 비교하며 설명하겠다 왜냐하면 가장 일반적인 네트워크라 생각하고 해당 블로그 글에서도 이더리움과 비교를 한다.)

이더리움은 단일 코인 이더로만 검증자로 참여가능하고 거래가 가능하다. 즉, 하나의 수단으로 사용하는 순간 다른 수단으로 사용을 못한다는 것이다. 즉, 묶인다는것이다.

![토큰](image-3.png)

그러지 말고 여러토큰들을 통해 거래도 가능하고 보안에도 기여할수있다면 고이지 않고 유동성이 늘어날수있지않을까?

어떻게 가능할지 알아보자 베라체인에는 다음과 같은 토큰 들이 존재한다.

BGT : 거버넌스 토큰 양도 불가능, 유저는 유동성 제공을 통해서만 얻을수있다.

BERA : 거래할때 사용되는 토큰

HONEY : 스테이블 코인

BGT 이 거버넌스 토큰이 베라체인의 핵심 토큰이다. BGT가 돌아가는 걸 보면 전체적으로 PoL의 구조를 이해할수있다.

![PoL](<스크린샷 2024-11-30 오전 2.09.39.png>)

1. 밸리데이터들은 블록을 만들고 BGT 스테이킹량만큼 보상을 나눠갖는다.
2. 밸리데이터는 원하는 Vault 에 자신이 받은 BGT를 나눠주고 해당 vault의 토큰 인센티브를 받아간다.
3. Vault는 받은 BGT를 사용자에게 나눠준다. 이때 사용자가 Vault에 넣은 LP 토큰의 지분 만큼 나눠준다.
4. 사용자는 Vault에게 받은 BGT를 다시 밸리데이터에게 위임하고 인센티브와 블록 보상(BGT)일부를 받는다.
5. 1번으로 다시돌아간다.

결국 서로가 나 이 이득을 챙기기 위해서 이게 더 필요해 하면서 이거 줄테니까 넌 이걸줘 하고있는것이다. 그게 BGT일수도 인센티브 일수도있다.

그리고 사용자는 자동으로 위임하면서 네트워크 보안에도 참여를 하고 풀도 간접적으로 참여를 하고 인센티브도 계속 돌고 BGT도 계속 돌고 유동성이 계속 도는 플라이휠 구조가 된다.

![PoL_2](image-4.png)

## 개인적인 생각

난 솔직히 DEX를 잘모른다. 그래서 엄청 자세히는 못다루겠지만 중요한건 문제점과 해결법에 어느정도 공감은 한다. 안정화 되지않은 프로토콜 작은 프로토콜들은 이 문제가 더 클거 같다. 그래서 해결법이 될수있을거 같다는게 지금 당장의 생각인데 중앙화의 문제는 없을지 한번더 생각해봐야겟다.
