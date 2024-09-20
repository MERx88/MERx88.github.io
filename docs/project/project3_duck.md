---
layout: default
title: Duck
parent: Project
nav_order: 3
---

# 멤버쉽 nft 프로젝트

개인 프로젝트
{: .label .label-green }
토이 프로젝트
{: .label .label-blue }

내 졸업프로젝트...잘할수있겠지...팀프로젝트지만 거의 혼자하는거라 개인프로젝트와 다름이 없다...

## 2024_09_19

프로젝트 목표

팬이 진심으로 해당 IP의 팬임을 인증할 수 있는 시스템과 데이터 주권을 보장하는 멤버쉽 플랫폼입니다. IP 소유자와 소비자 모두에게 상호 이익을 제공하며, 비공식 굿즈를 공식 인증 굿즈로 전환하여 새로운 가치를 창출합니다.

### 개같은 오류 Trouble Shooting

Trouble Shooting
{: .label .label-red }

아래와 같은 오류가 계속 뜬다 이유를 모르겠다. 예시 컨트랙트로 민팅을 날리는데 계속 파라미터가 잘못된다고 뜬다. 이 오류를 한번 고쳐보겠다. 개같은거 뒤졌다.

근데 사실 실제로 Dapp을 만들어보는건 처음이라 내가 역으로 싸먹힐수있다. 근데 열심히 노력해봐야지...

```
getContractError.js:34 Uncaught (in promise) ContractFunctionExecutionError: Invalid parameters were provided to the RPC method.
Double check you have provided the correct parameters.

Request Arguments:
  from:  0xae235446B9229c552766E37a67B16403499f31BB
  to:    0xe8E8dd120b067ba86cf82B711cC4Ca9F22C89EDc
  data:  0xd0def521000000000000000000000000ae235446b9229c552766e37a67b16403499f31bb00000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000035697066733a2f2f516d556f3941464e43673370777a333437585a3573734a3673575050336466587265697671763144714a4e66685a0000000000000000000000

Contract Call:
  address:   0xe8E8dd120b067ba86cf82B711cC4Ca9F22C89EDc
  function:  mint(address to, string customUri)
  args:          (0xae235446B9229c552766E37a67B16403499f31BB, ipfs://QmUo9AFNCg3pwz347XZ5ssJ6sWPP3dfXreivqv1DqJNfhZ)
  sender:    0xae235446B9229c552766E37a67B16403499f31BB

Docs: https://viem.sh/docs/contract/writeContract
Details: Invalid parameters: must provide an Ethereum address.
Version: 2.21.9
    at getContractError (getContractError.js:34:12)
    at writeContract (writeContract.js:88:98)
    at async mintNFT (AppContext.tsx:72:18)
    at async mintAndRegisterNFT (ResisterIPA.tsx:34:21)
Caused by: TransactionExecutionError: Invalid parameters were provided to the RPC method.
Double check you have provided the correct parameters.

Request Arguments:
  from:  0xae235446B9229c552766E37a67B16403499f31BB
  to:    0xe8E8dd120b067ba86cf82B711cC4Ca9F22C89EDc
  data:  0xd0def521000000000000000000000000ae235446b9229c552766e37a67b16403499f31bb00000000000000000000000000000000000000000000000000000000000000400000000000000000000000000000000000000000000000000000000000000035697066733a2f2f516d556f3941464e43673370777a333437585a3573734a3673575050336466587265697671763144714a4e66685a0000000000000000000000

Details: Invalid parameters: must provide an Ethereum address.
Version: 2.21.9
    at getTransactionError (getTransactionError.js:18:12)
    at sendTransaction (sendTransaction.js:179:105)
    at async writeContract (writeContract.js:80:16)
    at async mintNFT (AppContext.tsx:72:18)
    at async mintAndRegisterNFT (ResisterIPA.tsx:34:21)
Caused by: InvalidParamsRpcError: Invalid parameters were provided to the RPC method.
Double check you have provided the correct parameters.

Details: Invalid parameters: must provide an Ethereum address.
Version: 2.21.9
    at delay.count.count (buildRequest.js:49:31)
    at async attemptRetry (withRetry.js:17:30)
```

1. 파라미터를 모두 찍어 보았다. 근데 파라미터 솔직히 존나 잘보내고 있다.

- 이더리움 주소 : 0xae235446B9229c552766E37a67B16403499f31BB
- json 저장된 ipfs 주소 : ipfs://QmUo9AFNCg3pwz347XZ5ssJ6sWPP3dfXreivqv1DqJNfhZ

근데 대체 뭐가 문제지

![anya_serious](image-4.png)

솔직히 디버깅도 해보고 이거저것 해보았다. 컨트랙트 abi 를 보기 위해서 세폴리아 테넷까지 들어가서 확인해보았지만 없어서 그냥 내가 nft 컨트랙트 배포하고 만다 생각하고 컨트랙트 생성하기로 했다.

### ERC-721 배포하기

erc721에 어떤 함수가 있는지 어떻게 배포하는지 등은 알고 있다 물론 아주 오래전에 해서 기억이 가물가물 하다

우선 내가 컨트랙트 전체를 만들어서 진행하는건 개오바니 openzepplin 써서 만들려고한다. 일단 나는 배포를 위해 hardhat 사용하기로 했다.

그러고 컨트랙트 작성시작

우선 nft 기본 기능을 제외하고 오버라이딩해야하는 기능들? 그리고 추가해야하는 기능들을 생각해보았다.

1. 누구나 민팅가능
2. 무제한 발급
3. 이미지는 자신이 원하는 걸로

이는 그냥 내가 nft 만들었다는 것만 인증하고 이위에 나중에 story에서 제공하는 ipAsset으로 변환하기 위한 용도기에 요정도 기능이 필요했다.
