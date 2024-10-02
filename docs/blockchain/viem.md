---
layout: default
title: 🏛️ Viem
parent: Blockchain
nav_order: 3
---

# Viem

![viem](image.png)

web3, ethers 를 제친 녀석

## Client

블록체인과 상호작용하기 위해 사용되는 녀석

transport : 클라이언트가 요청을 만들면 이를 처리하고 블록체인으로 보내는 역할 반대로 블록체인에서 받아 클라이언트에게 넘기는 역할도 한다.

### 🚧🚧 Public Client 🌐 🚧🚧

공개 데이터 읽는 클라이언트

1. 이더리움 네트워크의 공개 데이터에 접근 가능
   -> 블록 번호나 계정 잔액 등등

2. public action으로 1번 활동을 가능하게 한다.

- getBlockNumber (현재 블록 번호 조회)
- getBalance (계정 잔액 조회)
- getTransaction (트랜잭션 정보 조회)

3. 서명 같은거 필요없음 -> 공개적이기 때문
4. 공개데이터 읽어올때 사용됨
5. HTTP 나 WebSocket등의 Transport를 사용해 JSON RPC API 로 요청을 보냄

### Wallet Client 🔒

거래실행 메세지서명등 말그대로 지갑과 연관있는 활동을 할수있는 기능을 제공하는 client다

- sendTransaction (트랜잭션 전송)
- signMessage (메세지 사인)

```js
import { createWalletClient, custom, parseEther } from 'viem'
import { mainnet } from 'viem/chains'

const client = createWalletClient({
  chain: mainnet,
  transport: custom(window.ethereum!)
})

const [address] = await client.getAddresses()

const hash = await client.sendTransaction({
  account: address,
  to: '0xa5cc3c03994DB5b0d9A5eEdD10CabaB0813678AC',
  value: parseEther('0.001')
})
```
