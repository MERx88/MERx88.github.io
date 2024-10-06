---
layout: default
title: 🔨 Foundry
parent: Blockchain
nav_order: 5
---

# 🔨 Foundry

## 2024_10_06

**foundry 특징**

- 모든 파일을 솔리디티로 작성가능 -> 테스트코드, 스크립트코드 전부 솔리디티로 작성가능하다.
- rust로 만들어져 있어 매우 빠른 속도를 자랑한다.

**foundry 컴파일**

`forge build` : 컴파일 명령어이다.

out 폴더 : 컨트랙트 ABI, 바이트코드 저장소

cashe 폴더 : 컴파일 프로세스를 용이하게 하는 임시 시스템 파일을 저장

### 스크립트 코드 작성하기

스크립트 코드를 작성하는 이유

- 배포 프로세스와 코드자체의 테스트를 향상 시킨다.
- 다양한 기능과 사용의 용이성을 향상 시킨다.

script폴더안에 만들며 .s.sol 접미사를 지닌다.

****

```js
// SPDX-License-Identifier: MIT

pragma solidity 0.8.19;

import {Script} from "forge-std/Script.sol";
import {SimpleStorage} from "../src/SimpleStorage.sol";

contract DeploySimpleStorage is Script {
    function run() external returns (SimpleStorage) {
        vm.startBroadcast(); //RPC URL로 전송될 트랜잭션 목록의 시작점

        SimpleStorage simpleStorage = new SimpleStorage(); //new로 새로운 계약 생성

        vm.stopBroadcast(); //RPC URL로 전송될 트랜잭션 목록의 끝점
        return simpleStorage; 
    }

}
```
- `import {Script} from "forge-std/Script.sol";`를 통해 Script를 가져와서 상속시켜야만 스크립트로 foundry가 간주한다.

- 모든 스크립트 파일은 메인 함수가 필요하며 이를 보통 run이라고 짓는다.

- vm 인스턴스를 통해 cheat codes를 사용 할수있다.

**스크립트 파일로 배포하기**

위와같이 스크립트 파일을 만들고 배포할준비가 끝나면 다음과 같은 명령어로 스크립트파일을 실행하고 배포할수있다.

조금씩 다르다 아래를 확인하자


1️⃣
```zsh 
forge script script/DeploySimpleStorage.s.sol 
```
anvil을 지가 알아서 실행하고 닫으면서 시뮬레이팅

2️⃣
```zsh 
forge script script/DeploySimpleStorage.s.sol --rpc-url http://127.0.0.1:8545 
```
돌아가는 anvil 위에서 시뮬레이팅

3️⃣
```zsh 
forge script script/DeploySimpleStorage.s.sol --rpc-url http://127.0.0.1:8545 --broadcast --private-key 0x...
```
돌아가는 anvil 위에 배포

**배포 트랜잭션 확인하기**

broadcast 폴더 : Foundry는 모든 블록체인 상호작용을 저장

dry-run 폴더 : 블록체인이 실행되고 있지 않을 때 수행한 상호작용 저장

broadcast/dry-run/(체인 Id)/run-latest.json 에 들어가면 아래와 같은 트랜잭션 정보를 확인할수있다.

```json
"transaction": {
    "from": "0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266",
    "to": null,
    "gas": "0x714e1",
    "value": "0x0",
    "input": "0x608060...c63430008130033",
    "nonce": "0x0",
    "chainId": "0x7a69",
    "accessList": null,
    "type": null
}
```
우리가 흔히아는 트랜잭션 필드이니까 넘어가는데 새로운거 하나만 짚고 넘어갈려한다


accessList : 이는 트랜잭션이 액세스할 가능성이 있는 주소와 관련된 저장소 키 목록을 포함하여 EVM이 트랜잭션 실행 중 저장소 접근 비용을 더 효율적으로 계산할 수 있도록 한다 라고 한다. 귀찮아서 복붙했다.😅 그니까 캐시마냥 기억해둬서 효율적으로 계산하는 필드다 뭐그런뜻이다