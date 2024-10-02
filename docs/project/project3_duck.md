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

### 민팅 오류 Trouble Shooting 🚀

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

솔직히 디버깅도 해보고 이거저것 해보았다. 컨트랙트 abi 를 보기 위해서 세폴리아 테넷까지 들어가서 확인해보았지만 없어서 내가 그냥 컨트랙트 만들고 말지! 이랬는데 다른 브라우저 환경에서는 잘되고 나만 안되는거여서 혹시 브라우저,.,,,? 초기화 하면 되지않을까 했는데 되었다...띠밤! 정말 열받는다.

## 2024_10_01

### IPA resister 오류 Trouble Shooting 🚀

Trouble Shooting
{: .label .label-red }

산넘어 산이다...

{: .warning-title }

> 오류 메세지
> Uncaught (in promise) Error: Failed to register IP: The wallet client does not have an account, please try again.
> at eval (story-protocol-react-sdk.esm.js:76:11)
> at async registerExistingNFT (ResisterIPA.tsx:65:22)

walletClient가 account가 없다고한다. 근데 난 지갑 연결 잘했는데? 🤷 그럼 민팅은 어캐하는건데 임마!

근데 우선 이 문제를 보면서 viem의 client에 대해서 더 찾아보았다.
