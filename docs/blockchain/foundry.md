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

---

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

## 2024_10_07

**CLI로 상호작용하기**

cast : CLI에서 해당 명령어를 사용하면 블록체인과 상호작용가능하다

```zsh
cast send 0x5FbDB2315678afecb367f032d93F642f64180aa3 "store(uint256)" 1337 --rpc-url $RPC_URL --private-key $PRIVATE_KEY
```

_cast send example_

```zsh
cast call 0x5FbDB2315678afecb367f032d93F642f64180aa3 "retrieve()"
```

_cast call example_

{ .important }
0x2 : EVM의 현재 기본 트랜잭션 타입

## 2024_10_08

**테스트 파일 작성하기**

test 폴더 안에 만들며 .t.sol 의 접미사를 지닌다.

```js
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.18;

import {Test, console} from "forge-std/Test.sol";

contract FundMeTest is Test {

    uint256 favNumber = 0;
    bool greatCourse = false;

    function setUp() external {
        favNumber = 1337;
        greatCourse = true;
        console.log("This will get printed first!");
    }

    function testDemo() public {
        assertEq(favNumber, 1337);
        assertEq(greatCourse, true);
        console.log("This will get printed second!");
        console.log("Updraft is changing lives!");
        console.log("You can print multiple things, for example this is a uint256, followed by a bool:", favNumber, greatCourse);
    }

 }
```

- `import {Test} from "forge-std/Test.sol";`를 통해 Script를 가져와서 상속시켜야만 스크립트로 foundry가 간주한다.

- setUp 함수 : 테스트 실행할때 가장 먼저 실행되는 함수 말그대로 테스트 시작하기전 세팅한다.

- console 라이브러리를 통해 디버깅 쌉가능

`forge test`라는 명령어를 통해 테스트 할수있으며 `forge test -vv`와 같이 verbosity를 설정해서 더 자세한 출력 로그를 출력할수있다. ( ✅ v의 갯수가 자세함을 결정한다.)

```js
// SPDX-License-Identifier: MIT
pragma solidity 0.8.27;

import {Test, console} from "forge-std/Test.sol";
import {FundMe} from "../src/FundMe.sol";

contract FundMeTest is Test {
    FundMe fundMe;

    function setUp() external {
        fundMe = new FundMe(msg.sender);
    }

    function testMinimumDollerisFive() public {
        assertEq(fundMe.MINIMUM_USD(), 5e18);
    }

    function testOwnerIsMsgSender() public {
        console.log(fundMe.getOwner());
        console.log(msg.sender);
        console.log(address(this));
        assertEq(fundMe.getOwner(), address(this));
    }
}

```

> 📌 FundMe 컨트랙트는 FundMeTest 컨트랙트에 의해 배포 되기 때문에 FundMe 컨트랙트의 소유자 역시 FundMeTest가 된다. msg.sender하고는 전혀 연관이 없다.
