---
layout: default
title: Viem
parent: Blockchain
nav_order: 3
---

# Viem

web3, ethers 를 제친 녀석

## Client

### Public Client

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
