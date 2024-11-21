---
layout: default
title: 🪅 Story Protocol
parent: Blockchain
nav_order: 2
---

# Story Protocol

저작권.,...레이어1! 아이피를 프로그래밍 가능!

## Table Of Contents

- [IP Asset](#ip-asset)
- [IP Account](#ip-account)
- [Module](#module)
- [Registry](#registry)
- [Programmable IP License](#programmable-ip-license)

## Concepts

### 🧩 IP Asset

그냥 말그대로 IP 이다. 짱구를 IP로 등록하고 싶다면 대표 NFT 발행하고 이를 등록하면 IP Asset이 된다.

**조금 더 자세히**

예시 정도 보면 메타데이터 이해 쌉가능

해리포터에 대한 IP Asset 메타데이터 Standard

```json
{
  "title": "Harry Potter and the Philosopher's Stone",
  "image": "link_to_book_cover",
  "dateCreatedISO8601": "1997-06-26T00:00:00", // June 26 1997
  "ipType": "literature",
  "creators": [
    {
      "name": "JK Rowling",
      "description": "Author",
      "socialMedia": [
        {
          "platform": "Wikipedia",
          "url": "https://en.wikipedia.org/wiki/J._K._Rowling"
        }
      ]
    },
    {
      "name": "Thomas Taylor",
      "description": "Illustrator"
    },
    {
      "name": "Bloomsbury Publishing",
      "description": "Publisher",
      "socialMedia": [
        {
          "platform": "Website",
          "url": "https://www.bloomsbury.com/"
        }
      ]
    }
  ],
  "media": [
    {
      "name": "ePub",
      "uri": "link_to_epub",
      "mimeType": "application/epub+zip"
    },
    {
      "name": "Book Summary PDF",
      "uri": "link_to_book_summary_pdf",
      "mimeType": "application/pdf"
    }
  ],
  "attributes": [
    {
      "key": "ISBN",
      "value": "978-0-7475-3269-0"
    },
    {
      "key": "Genre",
      "value": "Fantasy"
    }
  ]
}
```

### ⚙️ IP Account

IP Asset 연결된 스마트 컨트랙트!

- IP Asset의 데이터(라이선스 토큰, 로열티 토큰, 소유권 세부 정보 등)를 저장한다. -> 즉, 재료를 저장한다.
- 다양한 모듈에서 해당 데이터를 사용할수있도록 지원 (라이선싱, 수익/로열티 공유 등등) -> 프로그래밍 가능하기 때문에 더 다양한 작업 가능 -> 즉, 재료를 활용해 다양한 모듈을 가지고 기능을 수행
- 6551을 수정한 어��운트

<img src="../../assets/images/IPAImage.png" width="360px">

**조금 더 자세히**

모든 것의 기초가 되는 NFT가 이전되면 자동으로 IP Asset과 IP Account 모두 이전됨

### 🧱 Module

IP Account의 기능 을 확장 할수있는 스마트 컨트랙트 모듈

**핵심 모듈 3가지**
📜 라이선스 모듈
💸 로열티 모듈
❌ 분쟁 모듈

**조금 더 자세히**

[module interface](https://github.com/storyprotocol/protocol-core-v1/blob/main/contracts/interfaces/modules/base/IModule.sol)

위의 인터페이스를 준수하는 독립형 계약 모듈

### 🗂️ Registry

전역적으로 관리하는 디렉토리 스토리지 역할~ IP Account 보다는 더 큰 개념

### 💊 Programmable IP License (PIL)

실제 오프체인 법적 계약 이고 이걸 온체인 IP Asset에 첨부가능

## Module 살펴보기

### ⛏️ Base 모듈

모든 모듈에 대한 기본 기능을 담고 있음

```js
// SPDX-License-Identifier: BUSL-1.1
pragma solidity 0.8.26;

import { IERC165, ERC165 } from "@openzeppelin/contracts/utils/introspection/ERC165.sol";
import { IModule } from "../interfaces/modules/base/IModule.sol";

/// @title BaseModule
/// @notice Base implementation for all modules in Story Protocol.
abstract contract BaseModule is ERC165, IModule {
    /// @notice IERC165 interface support.
    function supportsInterface(bytes4 interfaceId) public view virtual override(ERC165, IERC165) returns (bool) {
        return interfaceId == type(IModule).interfaceId || super.supportsInterface(interfaceId);
    }
}
```

ERC165, IModule 을 상속받는다

ERC165는 다른 컨트랙트가 특정 인터페이스를 지원하는지 체크할수있게 해준다.

interdaceId가 Imodule의 인터페이스 ID와 일치하는 경우 true를 반환한다. 만약 그렇지 않으면 ERC165의 supportsInterface 함수를 호출하여 다른 인터페이스 지원 여부를 확인하게된다.

### 🧱 라이선스 모듈

IPAsset에 라이센스 모듈을 사용하면 해당 라이센스 조건에 따라 다른 사람이 사용하는 걸 제한할 수 있음

조금더 자세히 살펴보면 일단 현실세계에서 우리는 어떤 IP를 만들게 되면 해당 IP를 저작권으로 등록할수있고 IP에 대한 권리를 행사 할수있게 된다. 사실 라이센싱 모듈은 이게 다긴하다 근데 이제 컨트랙트와 블록체인으로 조리고 토큰으로 곁들인 느낌이다.

라이센스 모듈은 여러가지의 컨트랙트가 상호작용을 하면서 작동한다. 뭐당연한 이야기 이다. 코드를 집중적으로 살펴보기 전에 전반적으로 알아야 함수들이 무엇을 위해 쓰이는 지 알수있기에 한번 보자

**라이센스 템플릿**
템플릿이다. 말그대로 틀이다. 전체적인 약관에 대한 틀을 정의할수있다.

"Is commercial use allowed?" - true/false (bool)
"Is the license transferrable?" - true/false (bool)
"If commercial, what % of royalty do I receive?" - number

요런 느낌이다. 이렇게 정의 되어있는 라이센스 약관틀을 따르는 약관을 만들어서 나의 IP에 등록을 해서 저작권을 행사하는거라고 볼수있다. 지금은 스토리에서 개발한 PIL라고 하는 템플릿 밖에없다

약관을 등록하는 것은 기본이고 아래와 같은 기능또한 제공한다.

- 오프체인 법적 계약 템플릿 링크를 제공한다
- 무언가 작업할때 약관에 맞는지 확인하고 실행할수있는지 확인
- 부모와 자식 IP들의 호환성

**라이센스 약관**

앞에서 언급했던 약관에 대해서 좀 더 살펴보자

![LicenseTerms](image-2.png)

사실 앞의 내용을 이해했다면 해당 그림이 이해가될것이다. 붕어빵 틀에 슈크림을 넣거나 팥을 넣어서 붕어빵이라는 틀은 같지만 그안의 맛은 다르듯이 같은 약관 틀을 가지고 다른 약관들을 뽑아낸다.

이 약관은 처음 등록하면 절대 변경할수없다 절대로! 그리고 그림보면 아이디가 보이는데 이아이디를 통해 정의되어있느 약관을 재사용도 가능하다.

만약 파생 IP를 등록하면 부모 IP에서 약관을 상속 받게된다. 이떄 라이선스 토큰을 소각하고 약관을 상속받게 된다. 토큰이란 개념이 나오는데 바로 알아보자

**라이센스 토큰**

## 🗞️ PILicenseTemplate 해체분석

### 📜 BaseLicenseTemplateUpgradeable

라이선스 템플릿 기본 기능을 제공하는 컨트랙트 , 업그레이드 가능한 패턴이있다. 165 통해 인터페이스 지원을 관리한다.

```solidity
// SPDX-License-Identifier: BUSL-1.1
pragma solidity 0.8.26;

// external
import { ERC165 } from "@openzeppelin/contracts/utils/introspection/ERC165.sol";
import { IERC165 } from "@openzeppelin/contracts/utils/introspection/IERC165.sol";
import { Initializable } from "@openzeppelin/contracts-upgradeable/proxy/utils/Initializable.sol";
// contracts
import { ILicenseTemplate } from "../../interfaces/modules/licensing/ILicenseTemplate.sol";

//`Initializable` : 업그레이드 가능한 스마트 컨트랙트의 초기화 로직을 관리하는 기본 컨트랙트입니다. 이 컨트랙트는 프로토콜의 프록시 패턴을 지원하며, 초기화 함수와 관련된 다양한 수정자 및 상태 관리를 포함하고 있습니다.
//`ERC165` : 이더리움 스마트 컨트랙트에서 인터페이스 지원을 확인하기 위한 표준입니다. 이 표준은 특정 인터페이스가 구현되었는지를 확인할 수 있는 메커니즘을 제공합니다. 이를 통해 다른 컨트랙트와의 상호작용을 보다 안전하고 효율적으로 수행할 수 있습니다.
abstract contract BaseLicenseTemplateUpgradeable is ILicenseTemplate, ERC165, Initializable {
    /// @dev Storage structure for the BaseLicenseTemplateUpgradeable
    /// @custom:storage-location erc7201:story-protocol.BaseLicenseTemplateUpgradeable
    struct BaseLicenseTemplateUpgradeableStorage {
        string name;
        string metadataURI;
    }

    // keccak256(abi.encode(uint256(keccak256("story-protocol.BaseLicenseTemplateUpgradeable")) - 1)) &
    // ~bytes32(uint256(0xff));
    bytes32 private constant BaseLicenseTemplateUpgradeableStorageLocation =
        0x96c2f019b095cfe7c4d1f26aa9d2741961fe73294777688374a3299707c2fb00;


    // 👉 설명
    //컨트랙트 배포 시 초기화 함수를 비활성화합니다.
    //이는 프록시 패턴에서 구현 컨트랙트의 초기화를 방지하여 보안을 강화합니다.
    // 👉 특징: `@custom:oz-upgrades-unsafe-allow constructor` 주석을 통해 OpenZeppelin 업그레이드 도구에 의해 생성자가 안전하게 허용됨을 명시.
    /// @custom:oz-upgrades-unsafe-allow constructor
    constructor() {
        _disableInitializers();
    }


    // 👉 설명
    //라이선스 템플릿의 이름과 메타데이터 URI를 설정하는 내부 초기화 함수입니다.
    //`onlyInitializing` 제어자를 사용하여 초기화 과정에서만 호출될 수 있도록 제한합니다.
    // 👉 매개변수
    // `_name`: 라이선스 템플릿의 이름.
    // `_metadataURI`: 오프체인 메타데이터의 URL.
    // 👉 접근제한: `internal`
    /// @notice initializer for this implementation contract
    /// @param _name The name of the license template
    /// @param _metadataURI The URL to the off chain metadata
    function __BaseLicenseTemplate_init(string memory _name, string memory _metadataURI) internal onlyInitializing {
        _getBaseLicenseTemplateUpgradeableStorage().name = _name;
        _getBaseLicenseTemplateUpgradeableStorage().metadataURI = _metadataURI;
    }

    /// @notice Returns the name of the license template
    function name() public view override returns (string memory) {
        return _getBaseLicenseTemplateUpgradeableStorage().name;
    }

    /// @notice Returns the URL to the off chain metadata
    function getMetadataURI() public view override returns (string memory) {
        return _getBaseLicenseTemplateUpgradeableStorage().metadataURI;
    }

    // 👉 설명
    //컨트랙트가 특정 인터페이스를 지원하는지 확인합니다.
    //ERC-165 표준을 구현하여 다른 컨트랙트와의 호환성을 보장합니다.
    // 👉 매개변수
    // `interfaceId`: 확인하려는 인터페이스의 ID (`bytes4` 형식).
    // 👉 반환값: `bool`: 지원하면 `true`, 그렇지 않으면 `false`.
    // 👉 특징
    // `override` 키워드로 `ERC165`와 `IERC165`의 `supportsInterface` 함수를 재정의.
    // `ILicenseTemplate` 인터페이스를 지원하는지 여부를 먼저 확인한 후, 상위 컨트랙트의 구현을 호출.
    /// @notice IERC165 interface support.
    function supportsInterface(bytes4 interfaceId) public view virtual override(ERC165, IERC165) returns (bool) {
        return interfaceId == type(ILicenseTemplate).interfaceId || super.supportsInterface(interfaceId);
    }



    // 👉 설명: 저수준 어셈블리를 사용하여 네임스페이스된 스토리지 슬롯에서 `BaseLicenseTemplateUpgradeableStorage` 구조체에 접근합니다.
    // 👉 반환값: `BaseLicenseTemplateUpgradeableStorage storage $`: 스토리지 구조체의 참조.
    // 👉 특징
    // `private` 접근 제한으로 외부에서 호출 불가.
    // `ERC-7201 스토리지 패턴을 사용하여 스토리지 충돌을 방지.

    /// @dev Returns the storage struct of BaseLicenseTemplateUpgradeable.
    function _getBaseLicenseTemplateUpgradeableStorage()
        private
        pure
        returns (BaseLicenseTemplateUpgradeableStorage storage $)
    {
        assembly {
            $.slot := BaseLicenseTemplateUpgradeableStorageLocation
        }
    }
}
```

### 📜 ILicenseTemplate

당연히 인터페이스의 기능을 하며 라이선스 조건 등록 관리 기능을 제공하는 인터페이스다

```solidity
// SPDX-License-Identifier: BUSL-1.1
pragma solidity 0.8.26;

import { IERC165 } from "@openzeppelin/contracts/interfaces/IERC165.sol";

/// @title ILicenseTemplate
/// @notice This interface defines the methods for a License Template.
/// A License Template is responsible for defining a template of license terms that allow users to create
/// licenses based on the template terms.
/// The License Template contract is also responsible for registering, storing, verifying,
/// and displaying license terms registered with the License Template.
/// Anyone can implement a License Template and register it into the Story Protocol.
/// @dev The License Template should assign an unique ID to each license terms registered.
interface ILicenseTemplate is IERC165 {
    /// @notice Emitted when a new license terms is registered.
    /// @param licenseTermsId The ID of the license terms.
    /// @param licenseTemplate The address of the license template.
    /// @param licenseTerms The data of the license.
    event LicenseTermsRegistered(uint256 indexed licenseTermsId, address indexed licenseTemplate, bytes licenseTerms);

    /// @notice Returns the name of the license template.
    /// @return The name of the license template.
    function name() external view returns (string memory);

    /// @notice Converts the license terms to a JSON string which will be part of the metadata of license token.
    /// @dev the json will be part of metadata as attributes return by tokenURI() license token,
    /// hence the json format should follow the common NFT metadata standard.
    /// @param licenseTermsId The ID of the license terms.
    /// @return The JSON string of the license terms.
    function toJson(uint256 licenseTermsId) external view returns (string memory);

    /// @notice Returns the metadata URI of the license template.
    /// @return The metadata URI of the license template.
    function getMetadataURI() external view returns (string memory);

    /// @notice Returns the URI of the license terms.
    /// @param licenseTermsId The ID of the license terms.
    /// @return The URI of the license terms.
    function getLicenseTermsURI(uint256 licenseTermsId) external view returns (string memory);

    /// @notice Returns the total number of registered license terms.
    /// @return The total number of registered license terms.
    function totalRegisteredLicenseTerms() external view returns (uint256);

    // 👉 설명: 특정 라이선스 조건이 존재하는지 확인합니다.
    // 👉 매개변수: `licenseTermsId`: 라이선스 조건의 ID.
    // 👉 반환값: `bool`: 존재하면 `true`, 아니면 `false`.
    /// @notice Checks if a license terms exists.
    /// @param licenseTermsId The ID of the license terms.
    /// @return True if the license terms exists, false otherwise.
    function exists(uint256 licenseTermsId) external view returns (bool);

    /// @notice Checks if a license terms is transferable.
    /// @param licenseTermsId The ID of the license terms.
    /// @return True if the license terms is transferable, false otherwise.
    function isLicenseTransferable(uint256 licenseTermsId) external view returns (bool);

    // 👉 설명: 주어진 라이선스 조건들 중 가장 이른 만료 시간을 반환합니다.
    // 👉 매개변수
    // `licenseTermsIds`: 라이선스 조건의 ID 배열.
    // `start`: 만료 시간 계산의 시작 시간.
    // 👉 반환값: `uint256`: 가장 이른 만료 시간.
    /// @notice Returns the earliest expiration time among the given license terms.
    /// @param start The start time to calculate the expiration time.
    /// @param licenseTermsIds The IDs of the license terms.
    /// @return The earliest expiration time.
    function getEarlierExpireTime(uint256[] calldata licenseTermsIds, uint256 start) external view returns (uint256);

    /// @notice Returns the expiration time of a license terms.
    /// @param start The start time.
    /// @param licenseTermsId The ID of the license terms.
    /// @return The expiration time.
    function getExpireTime(uint256 licenseTermsId, uint256 start) external view returns (uint256);

    /// @notice Returns the royalty policy of a license terms.
    /// @dev All License Templates should implement this method.
    /// The royalty policy is used to calculate royalties and pay minting license fee.
    /// Should return address(0) if the license template does not support a royalty policy or
    /// the license term does set RoyaltyPolicy.
    /// @param licenseTermsId The ID of the license terms.
    /// @return royaltyPolicy The address of the royalty policy specified for the license terms.
    /// @return royaltyPercent The percentage of the royalty.
    /// @return mintingLicenseFee The fee for minting a license.
    /// @return currencyToken The address of the ERC20 token, used for minting license fee and royalties.
    /// the currency token will used for pay for license token minting fee and royalties.
    function getRoyaltyPolicy(
        uint256 licenseTermsId
    )
        external
        view
        returns (address royaltyPolicy, uint32 royaltyPercent, uint256 mintingLicenseFee, address currencyToken);

    // 👉 설명: 라이선스 토큰의 발행을 검증합니다.
    // 👉 매개변수
    // `amount`: 발행할 라이선스 수량.
    // `licensorIpId`: 라이선스 제공자의 IP ID.
    // `licenseTermsId`: 라이선스 조건의 ID.
    // `licensee`: 라이선스 수령자의 주소.
    // 👉 반환값: `bool`: 검증 성공 시 `true`, 실패 시 `false`.
    /// @notice Verifies the minting of a license token.
    /// @dev the function will be called by the LicensingModule when minting a license token to
    /// verify the minting is whether allowed by the license terms.
    /// @param licenseTermsId The ID of the license terms.
    /// @param licensee The address of the licensee who will receive the license token.
    /// @param licensorIpId The IP ID of the licensor who attached the license terms minting the license token.
    /// @param amount The amount of licenses to mint.
    /// @return True if the minting is verified, false otherwise.
    function verifyMintLicenseToken(
        uint256 licenseTermsId,
        address licensee,
        address licensorIpId,
        uint256 amount
    ) external returns (bool);


    // 👉 설명: 파생 작품의 등록을 검증합니다.
    // 👉 매개변수
    // `childIpId`: 파생 작품의 IP ID.
    // `parentIpId`: 원본 IP의 ID 배열.
    // `licenseTermsId`: 라이선스 조건의 ID.
    // `licensee`: 라이선스 수령자의 주소.
    // 👉 반환값: `bool`: 검증 성공 시 `true`, 실패 시 `false`.
    /// @notice Verifies the registration of a derivative.
    /// @dev This function is invoked by the LicensingModule during the registration of a derivative work
    //// to ensure compliance with the parent intellectual property's licensing terms.
    /// It verifies whether the derivative's registration is permitted under those terms.
    /// @param childIpId The IP ID of the derivative.
    /// @param parentIpId The IP ID of the parent.
    /// @param licenseTermsId The ID of the license terms.
    /// @param licensee The address of the licensee.
    /// @return True if the registration is verified, false otherwise.
    function verifyRegisterDerivative(
        address childIpId,
        address parentIpId,
        uint256 licenseTermsId,
        address licensee
    ) external returns (bool);

    // 👉 설명: 여러 라이선스 조건의 호환성을 검증합니다.
    // 👉 매개변수: `licenseTermsIds`: 라이선스 조건의 ID 배열.
    // 👉 반환값: `bool`: 호환 가능하면 `true`, 아니면 `false`.
    /// @notice Verifies if the licenses are compatible.
    /// @dev This function is called by the LicensingModule to verify license compatibility
    /// when registering a derivative IP to multiple parent IPs.
    /// It ensures that the licenses of all parent IPs are compatible with each other during the registration process.
    /// @param licenseTermsIds The IDs of the license terms.
    /// @return True if the licenses are compatible, false otherwise.
    function verifyCompatibleLicenses(uint256[] calldata licenseTermsIds) external view returns (bool);

    // 👉 설명: 모든 원본 IP의 라이선스 조건을 준수하는지 검증합니다.
    // 👉 매개변수
    // `childIpId`: 파생 작품의 IP ID.
    // `parentIpId`: 원본 IP의 ID 배열.
    // `licenseTermsIds`: 라이선스 조건의 ID 배열.
    // `childIpOwner`: 파생 작품 소유자의 주소.
    // 👉 반환값: `bool`: 검증 성공 시 `true`, 실패 시 `false`.
    /// @notice Verifies the registration of a derivative for all parent IPs.
    /// @dev This function is called by the LicensingModule to verify licenses for registering a derivative IP
    /// to multiple parent IPs.
    /// the function will verify the derivative for each parent IP's license and
    /// also verify all licenses are compatible.
    /// @param childIpId The IP ID of the derivative.
    /// @param parentIpId The IP IDs of the parents.
    /// @param licenseTermsIds The IDs of the license terms.
    /// @param childIpOwner The address of the derivative IP owner.
    /// @return True if the registration is verified, false otherwise.
    function verifyRegisterDerivativeForAllParents(
        address childIpId,
        address[] calldata parentIpId,
        uint256[] calldata licenseTermsIds,
        address childIpOwner
    ) external returns (bool);
}
```

### 📜 IPILicenseTemplate

```solidity

// SPDX-License-Identifier: BUSL-1.1
pragma solidity 0.8.26;

import { ILicenseTemplate } from "../../../interfaces/modules/licensing/ILicenseTemplate.sol";

/// @notice 이 구조체는 프로그래머블 IP 라이선스(PIL)의 조건을 정의합니다.
/// 이 조건은 IP 자산에 첨부될 수 있습니다. PIL의 법적 문서는 이 저장소에서 확인할 수 있습니다.
/// @param transferable 라이선스가 양도 가능한지 여부를 나타냅니다.
/// @param royaltyPolicy StoryProtocol에 사전 요구되는 로열티 정책 계약의 주소입니다.
/// @param mintingFee 라이선스를 발행할 때 지불해야 하는 수수료입니다.
/// @param expiration 라이선스의 만료 기간입니다.
/// @param commercialUse 작업이 상업적으로 사용될 수 있는지 여부를 나타냅니다.
/// @param commercialAttribution 작업을 상업적으로 재생산할 때 저작권 표시가 필요한지 여부입니다.
/// @param commercializerChecker 상업적으로 작업을 활용할 수 있는 상업화자입니다. 제로 주소인 경우,
/// 제한이 적용되지 않습니다.
/// @param commercializerCheckerData 상업화자 검사 계약에 전달될 데이터입니다.
/// @param commercialRevShare 라이선스 제공자와 공유해야 하는 수익의 비율입니다.
/// @param commercialRevCeiling 작업의 상업적 사용으로 생성될 수 있는 최대 수익입니다.
/// @param derivativesAllowed 라이선스 수령자가 자신의 작업의 파생물을 생성할 수 있는지 여부를 나타냅니다.
/// @param derivativesAttribution 파생물에 대한 저작권 표시가 필요한지 여부입니다.
/// @param derivativesApproval 라이선스 제공자가 작업의 파생물이 라이선스 제공자의 IP ID에 연결되기 전에
/// 승인해야 하는지 여부입니다.
/// @param derivativesReciprocal 라이선스 수령자가 작업의 파생물을 동일한 조건으로 라이선스해야 하는지 여부입니다.
/// @param derivativeRevCeiling 파생물 사용으로 생성될 수 있는 최대 수익입니다.
/// @param currency 발행 수수료를 지불하는 데 사용될 ERC20 토큰입니다. 이 토큰은 Story Protocol에 등록되어야 합니다.
/// @param uri 라이선스 조건의 URI로, 오프체인 라이선스 조건을 가져오는 데 사용될 수 있습니다.

struct PILTerms {
    bool transferable;
    address royaltyPolicy;
    uint256 defaultMintingFee;
    uint256 expiration;
    bool commercialUse;
    bool commercialAttribution;
    address commercializerChecker;
    bytes commercializerCheckerData;
    uint32 commercialRevShare;
    uint256 commercialRevCeiling;
    bool derivativesAllowed;
    bool derivativesAttribution;
    bool derivativesApproval;
    bool derivativesReciprocal;
    uint256 derivativeRevCeiling;
    address currency;
    string uri;
}

/// @title IPILicenseTemplate
/// @notice This interface defines the methods for a Programmable IP License (PIL) template.
/// The PIL template is used to generate PIL terms that can be attached to IP Assets.
/// The legal document of the PIL can be found in this repository.
interface IPILicenseTemplate is ILicenseTemplate {
    /// @notice Registers new license terms.
    /// @param terms The PILTerms to register.
    /// @return selectedLicenseTermsId The ID of the newly registered license terms.
    function registerLicenseTerms(PILTerms calldata terms) external returns (uint256 selectedLicenseTermsId);

    /// @notice Gets the ID of the given license terms.
    /// @param terms The PILTerms to get the ID for.
    /// @return selectedLicenseTermsId The ID of the given license terms.
    function getLicenseTermsId(PILTerms calldata terms) external view returns (uint256 selectedLicenseTermsId);

    /// @notice Gets license terms of the given ID.
    /// @param selectedLicenseTermsId The ID of the license terms.
    /// @return terms The PILTerms associate with the given ID.
    function getLicenseTerms(uint256 selectedLicenseTermsId) external view returns (PILTerms memory terms);
}


```

### 📜 LicensorApprovalChecker

해당 컨트랙트는 부모 IP Account 가 자식 IP Account 승인을 관리하는 기능을 제공

```solidity
// SPDX-License-Identifier: BUSL-1.1
pragma solidity 0.8.26;

import { AccessControlled } from "../../../access/AccessControlled.sol";
import { Initializable } from "@openzeppelin/contracts-upgradeable/proxy/utils/Initializable.sol";

/// @title LicensorApprovalChecker
/// @notice Manages the approval of derivative IP accounts by the parentIp. Used to verify
/// licensing terms like "Derivatives With Approval" in PIL.
abstract contract LicensorApprovalChecker is AccessControlled, Initializable {
    /// @notice Emits when a derivative IP account is approved by the parentIp.
    /// @param licenseTermsId The ID of the license waiting for approval
    /// @param ipId The ID of the derivative IP to be approved
    /// @param caller The executor of the approval
    /// @param approved Result of the approval
    event DerivativeApproved(
        uint256 indexed licenseTermsId,
        address indexed ipId,
        address indexed caller,
        bool approved
    );

    /// @notice Storage for derivative IP approvals.
    /// @param approvals Approvals for derivative IP.
    /// @dev License Id => parentIpId => childIpId => approved
    /// @custom:storage-location erc7201:story-protocol.LicensorApprovalChecker
    struct LicensorApprovalCheckerStorage {
        mapping(uint256 => mapping(address => mapping(address => bool))) approvals;
    }

    // keccak256(abi.encode(uint256(keccak256("story-protocol.LicensorApprovalChecker")) - 1))
    // & ~bytes32(uint256(0xff));
    bytes32 private constant LicensorApprovalCheckerStorageLocation =
        0x7a71306cccadc52d66a0a466930bd537acf0ba900f21654919d58cece4cf9500;

    /// @notice Constructor function
    /// @param accessController The address of the AccessController contract
    /// @param ipAccountRegistry The address of the IPAccountRegistry contract
    /// @custom:oz-upgrades-unsafe-allow constructor
    constructor(
        address accessController,
        address ipAccountRegistry
    ) AccessControlled(accessController, ipAccountRegistry) {}

    // 👉 설명: 외부에서 호출할 수 있는 함수로, 파라미터로 받은 정보를 바탕으로 자식 IP 계정에 대한 승인을 설정합니다.
    // 👉 매개변수
    // parentIpId: 부모 IP의 ID
    // licenseTermsId: 승인을 기다리는 라이센스의 ID
    // childIpId: 승인할 자식 IP의 ID
    // approved: 승인 여부 (true/false)
    /// @notice Approves or disapproves a derivative IP account.
    /// @param parentIpId The ID of the parent IP grant the approval
    /// @param licenseTermsId The ID of the license waiting for approval
    /// @param childIpId The ID of the derivative IP to be approved
    /// @param approved Result of the approval
    function setApproval(address parentIpId, uint256 licenseTermsId, address childIpId, bool approved) external {
        _setApproval(parentIpId, licenseTermsId, childIpId, approved);
    }


   // 👉 설명: 특정 자식 IP 계정이 부모에 의해 승인되었는지를 확인하는 함수입니다.
    // 👉 매개변수
    // parentIpId: 부모 IP의 ID
    // licenseTermsId: 라이센스의 ID
    // childIpId: 승인할 자식 IP의 ID
    // 👉 반환값: `bool`: 자식 IP 계정이 승인되었으면 `true`, 실패 시 `false`.
    // 👉 저장소 접근: _getLicensorApprovalCheckerStorage를 통해 저장소에 접근하여 승인 상태를 조회합니다.
    /// @notice Checks if a derivative IP account is approved by the parent.
    /// @param licenseTermsId The ID of the license NFT issued from a policy of the parent
    /// @param childIpId The ID of the derivative IP to be approved
    /// @return approved True if the derivative IP account using the license is approved
    function isDerivativeApproved(
        address parentIpId,
        uint256 licenseTermsId,
        address childIpId
    ) public view returns (bool) {
        LicensorApprovalCheckerStorage storage $ = _getLicensorApprovalCheckerStorage();
        return $.approvals[licenseTermsId][parentIpId][childIpId];
    }


    // 👉 설명: 내부에서 호출되는 함수로, 자식 IP 계정에 대한 승인을 설정합니다.
    // 👉 매개변수
    // parentIpId: 부모 IP의 ID
    // licenseTermsId: 승인을 기다리는 라이센스의 ID
    // childIpId: 승인할 자식 IP의 ID
    // approved: 승인 여부 (true/false)
    // 👉 제어: verifyPermission 수정자를 사용하여 호출자가 부모 IP 계정인지 확인합니다.
    // 👉 저장소 업데이트: 승인 상태를 저장소에 업데이트하고, DerivativeApproved 이벤트를 발생시킵니다.
    /// @notice Sets the approval for a derivative IP account.
    /// @dev This function is only callable by the parent IP account.
    /// @param parentIpId The ID of the parent IP account
    /// @param licenseTermsId The ID of the license waiting for approval
    /// @param childIpId The ID of the derivative IP to be approved
    /// @param approved Result of the approval
    function _setApproval(
        address parentIpId,
        uint256 licenseTermsId,
        address childIpId,
        bool approved
    ) internal verifyPermission(parentIpId) {
        LicensorApprovalCheckerStorage storage $ = _getLicensorApprovalCheckerStorage();
        $.approvals[licenseTermsId][parentIpId][childIpId] = approved;
        emit DerivativeApproved(licenseTermsId, parentIpId, msg.sender, approved);
    }

    // 👉 설명: LicensorApprovalCheckerStorage 구조체의 저장소 위치를 반환하는 함수입니다.
    // 👉 특징: 어셈블리 코드를 사용하여 특정 슬롯에 대한 접근을 설정합니다. 이로 인해 저장소에 직접 접근할 수 있습니다.
    /// @notice Sets the approval for a derivative IP account.
    /// @dev Returns the storage struct of LicensorApprovalChecker.
    function _getLicensorApprovalCheckerStorage() private pure returns (LicensorApprovalCheckerStorage storage $) {
        assembly {
            $.slot := LicensorApprovalCheckerStorageLocation
        }
    }
}
```

### 📜 AccessManagedUpgradeable

```solidity
// SPDX-License-Identifier: MIT
// OpenZeppelin Contracts (last updated v5.0.0) (access/manager/AccessManaged.sol)

pragma solidity ^0.8.20;

import {IAuthority} from "@openzeppelin/contracts/access/manager/IAuthority.sol";
import {AuthorityUtils} from "@openzeppelin/contracts/access/manager/AuthorityUtils.sol";
import {IAccessManager} from "@openzeppelin/contracts/access/manager/IAccessManager.sol";
import {IAccessManaged} from "@openzeppelin/contracts/access/manager/IAccessManaged.sol";
import {ContextUpgradeable} from "../../utils/ContextUpgradeable.sol";
import {Initializable} from "../../proxy/utils/Initializable.sol";

/**
 * @dev This contract module makes available a {restricted} modifier. Functions decorated with this modifier will be
 * permissioned according to an "authority": a contract like {AccessManager} that follows the {IAuthority} interface,
 * implementing a policy that allows certain callers to access certain functions.
 *
 * IMPORTANT: The `restricted` modifier should never be used on `internal` functions, judiciously used in `public`
 * functions, and ideally only used in `external` functions. See {restricted}.
 */
abstract contract AccessManagedUpgradeable is Initializable, ContextUpgradeable, IAccessManaged {
    /// @custom:storage-location erc7201:openzeppelin.storage.AccessManaged
    struct AccessManagedStorage {
        address _authority;

        bool _consumingSchedule;
    }

    // keccak256(abi.encode(uint256(keccak256("openzeppelin.storage.AccessManaged")) - 1)) & ~bytes32(uint256(0xff))
    bytes32 private constant AccessManagedStorageLocation = 0xf3177357ab46d8af007ab3fdb9af81da189e1068fefdc0073dca88a2cab40a00;

    function _getAccessManagedStorage() private pure returns (AccessManagedStorage storage $) {
        assembly {
            $.slot := AccessManagedStorageLocation
        }
    }


    // 👉 설명: 초기 권한을 설정하는 함수입니다.
    /**
     * @dev Initializes the contract connected to an initial authority.
     */
    function __AccessManaged_init(address initialAuthority) internal onlyInitializing {
        __AccessManaged_init_unchained(initialAuthority);
    }

    function __AccessManaged_init_unchained(address initialAuthority) internal onlyInitializing {
        _setAuthority(initialAuthority);
    }

    /**
     * @dev Restricts access to a function as defined by the connected Authority for this contract and the
     * caller and selector of the function that entered the contract.
     *
     * [IMPORTANT]
     * ====
     * In general, this modifier should only be used on `external` functions. It is okay to use it on `public`
     * functions that are used as external entry points and are not called internally. Unless you know what you're
     * doing, it should never be used on `internal` functions. Failure to follow these rules can have critical security
     * implications! This is because the permissions are determined by the function that entered the contract, i.e. the
     * function at the bottom of the call stack, and not the function where the modifier is visible in the source code.
     * ====
     *
     * [WARNING]
     * ====
     * Avoid adding this modifier to the https://docs.soliditylang.org/en/v0.8.20/contracts.html#receive-ether-function[`receive()`]
     * function or the https://docs.soliditylang.org/en/v0.8.20/contracts.html#fallback-function[`fallback()`]. These
     * functions are the only execution paths where a function selector cannot be unambiguosly determined from the calldata
     * since the selector defaults to `0x00000000` in the `receive()` function and similarly in the `fallback()` function
     * if no calldata is provided. (See {_checkCanCall}).
     *
     * The `receive()` function will always panic whereas the `fallback()` may panic depending on the calldata length.
     * ====
     */
    // 👉 설명: 이 수정자가 적용된 함수는 호출자가 권한이 있는지 확인합니다.
    // 👉 중요:`internal` 함수에는 사용하지 않아야 하며, `public` 또는 `external` 함수에서만 사용해야 합니다.
    modifier restricted() {
        _checkCanCall(_msgSender(), _msgData());
        _;
    }

    // 👉 설명: 권한관련 함수들
    /// @inheritdoc IAccessManaged
    function authority() public view virtual returns (address) {
        AccessManagedStorage storage $ = _getAccessManagedStorage();
        return $._authority;
    }

    /// @inheritdoc IAccessManaged
    function setAuthority(address newAuthority) public virtual {
        address caller = _msgSender();
        if (caller != authority()) {
            revert AccessManagedUnauthorized(caller);
        }
        if (newAuthority.code.length == 0) {
            revert AccessManagedInvalidAuthority(newAuthority);
        }
        _setAuthority(newAuthority);
    }
    // 👉 설명: 현재 소비 중인 스케줄 작업이 있는지 확인합니다.
    /// @inheritdoc IAccessManaged
    function isConsumingScheduledOp() public view returns (bytes4) {
        AccessManagedStorage storage $ = _getAccessManagedStorage();
        return $._consumingSchedule ? this.isConsumingScheduledOp.selector : bytes4(0);
    }

    /**
     * @dev Transfers control to a new authority. Internal function with no access restriction. Allows bypassing the
     * permissions set by the current authority.
     */
    function _setAuthority(address newAuthority) internal virtual {
        AccessManagedStorage storage $ = _getAccessManagedStorage();
        $._authority = newAuthority;
        emit AuthorityUpdated(newAuthority);
    }

    // 👉 설명: 호출자가 특정 함수에 접근할 수 있는지 확인합니다. 호출자가 권한이 없으면 오류를 발생시킵니다.
    /**
     * @dev Reverts if the caller is not allowed to call the function identified by a selector. Panics if the calldata
     * is less than 4 bytes long.
     */
    function _checkCanCall(address caller, bytes calldata data) internal virtual {
        AccessManagedStorage storage $ = _getAccessManagedStorage();
        (bool immediate, uint32 delay) = AuthorityUtils.canCallWithDelay(
            authority(),
            caller,
            address(this),
            bytes4(data[0:4])
        );
        if (!immediate) {
            if (delay > 0) {
                $._consumingSchedule = true;
                IAccessManager(authority()).consumeScheduledOp(caller, data);
                $._consumingSchedule = false;
            } else {
                revert AccessManagedUnauthorized(caller);
            }
        }
    }
}

```

### 📜 ReentrancyGuardUpgradeable

재진입 공격을 방지하기 위한 기능을 제공하는 추상 컨트랙트

해당 컨트랙트를 상속받으면 `nonReentrant` modifier 사용할 수 있어, 특정 함수가 중첩 호출되는 것을 방지할수있다. -> 보안이 강화된다.

```solidity
// SPDX-License-Identifier: MIT
// OpenZeppelin Contracts (last updated v5.0.0) (utils/ReentrancyGuard.sol)

pragma solidity ^0.8.20;
import {Initializable} from "../proxy/utils/Initializable.sol";

/**
 * @dev Contract module that helps prevent reentrant calls to a function.
 *
 * Inheriting from `ReentrancyGuard` will make the {nonReentrant} modifier
 * available, which can be applied to functions to make sure there are no nested
 * (reentrant) calls to them.
 *
 * Note that because there is a single `nonReentrant` guard, functions marked as
 * `nonReentrant` may not call one another. This can be worked around by making
 * those functions `private`, and then adding `external` `nonReentrant` entry
 * points to them.
 *
 * TIP: If you would like to learn more about reentrancy and alternative ways
 * to protect against it, check out our blog post
 * https://blog.openzeppelin.com/reentrancy-after-istanbul/[Reentrancy After Istanbul].
 */
abstract contract ReentrancyGuardUpgradeable is Initializable {
    // Booleans are more expensive than uint256 or any type that takes up a full
    // word because each write operation emits an extra SLOAD to first read the
    // slot's contents, replace the bits taken up by the boolean, and then write
    // back. This is the compiler's defense against contract upgrades and
    // pointer aliasing, and it cannot be disabled.


    // 👉 설명: 재진입 상태를 나타내는 상수입니다. `NOT_ENTERED`는 함수가 호출되지 않은 상태를, `ENTERED`는 함수가 호출된 상태를 나타냅니다.
    // The values being non-zero value makes deployment a bit more expensive,
    // but in exchange the refund on every call to nonReentrant will be lower in
    // amount. Since refunds are capped to a percentage of the total
    // transaction's gas, it is best to keep them low in cases like this one, to
    // increase the likelihood of the full refund coming into effect.
    uint256 private constant NOT_ENTERED = 1;
    uint256 private constant ENTERED = 2;

    // 👉 설명: 재진입 상태를 저장하는 구조체입니다.
    /// @custom:storage-location erc7201:openzeppelin.storage.ReentrancyGuard
    struct ReentrancyGuardStorage {
        uint256 _status;
    }
    // 👉 설명: ERC-7201 네임스페이스를 사용하여 스토리지 충돌을 방지합니다.
    // keccak256(abi.encode(uint256(keccak256("openzeppelin.storage.ReentrancyGuard")) - 1)) & ~bytes32(uint256(0xff))
    bytes32 private constant ReentrancyGuardStorageLocation = 0x9b779b17422d0df92223018b32b4d1fa46e071723d6817e2486d003becc55f00;

    function _getReentrancyGuardStorage() private pure returns (ReentrancyGuardStorage storage $) {
        assembly {
            $.slot := ReentrancyGuardStorageLocation
        }
    }
    // 👉 설명: 재진입 호출이 발생했을 때 발생하는 오류입니다.
    /**
     * @dev Unauthorized reentrant call.
     */
    error ReentrancyGuardReentrantCall();

    // 👉 설명: 재진입 방지 기능을 초기화하는 함수입니다.
    function __ReentrancyGuard_init() internal onlyInitializing {
        __ReentrancyGuard_init_unchained();
    }

    function __ReentrancyGuard_init_unchained() internal onlyInitializing {
        ReentrancyGuardStorage storage $ = _getReentrancyGuardStorage();
        $._status = NOT_ENTERED;
    }

    // 👉 설명: 이 수정자가 적용된 함수는 재진입을 방지합니다. 함수가 호출되기 전에 `_nonReentrantBefore`가 실행되고, 호출이 끝난 후 `_nonReentrantAfter`가 실행됩니다.
    /**
     * @dev Prevents a contract from calling itself, directly or indirectly.
     * Calling a `nonReentrant` function from another `nonReentrant`
     * function is not supported. It is possible to prevent this from happening
     * by making the `nonReentrant` function external, and making it call a
     * `private` function that does the actual work.
     */
    modifier nonReentrant() {
        _nonReentrantBefore();
        _;
        _nonReentrantAfter();
    }
    // 👉 설명: 함수 호출 전에 재진입 상태를 확인하고, 이미 호출된 상태라면 오류를 발생시킵니다.
    function _nonReentrantBefore() private {
        ReentrancyGuardStorage storage $ = _getReentrancyGuardStorage();
        // On the first call to nonReentrant, _status will be NOT_ENTERED
        if ($._status == ENTERED) {
            revert ReentrancyGuardReentrantCall();
        }

        // Any calls to nonReentrant after this point will fail
        $._status = ENTERED;
    }
    // 👉 설명: 함수 호출 후 재진입 상태를 초기화합니다.
    function _nonReentrantAfter() private {
        ReentrancyGuardStorage storage $ = _getReentrancyGuardStorage();
        // By storing the original value once again, a refund is triggered (see
        // https://eips.ethereum.org/EIPS/eip-2200)
        $._status = NOT_ENTERED;
    }
    // 👉 설명: 현재 재진입 상태가 `ENTERED`인지 확인하여, 재진입이 발생했는지를 반환합니다.
    /**
     * @dev Returns true if the reentrancy guard is currently set to "entered", which indicates there is a
     * `nonReentrant` function in the call stack.
     */
    function _reentrancyGuardEntered() internal view returns (bool) {
        ReentrancyGuardStorage storage $ = _getReentrancyGuardStorage();
        return $._status == ENTERED;
    }
}

```

### 📜 UUPSUpgradeable

컨트랙트는 UUPS(Universal Upgradeable Proxy Standard) 프록시를 위한 업그레이드 메커니즘을 제공하는 추상 컨트랙트이다. 해당 컨트랙트는 업그레이드 가능한 스마트 컨트랙트의 구현을 관리하고, 특정 함수가 호출될 때 권한을 확인하는 기능을 포함한다.

````solidity
// SPDX-License-Identifier: MIT
// OpenZeppelin Contracts (last updated v5.0.0) (proxy/utils/UUPSUpgradeable.sol)

pragma solidity ^0.8.20;

import {IERC1822Proxiable} from "@openzeppelin/contracts/interfaces/draft-IERC1822.sol";
import {ERC1967Utils} from "@openzeppelin/contracts/proxy/ERC1967/ERC1967Utils.sol";
import {Initializable} from "./Initializable.sol";

/**
 * @dev An upgradeability mechanism designed for UUPS proxies. The functions included here can perform an upgrade of an
 * {ERC1967Proxy}, when this contract is set as the implementation behind such a proxy.
 *
 * A security mechanism ensures that an upgrade does not turn off upgradeability accidentally, although this risk is
 * reinstated if the upgrade retains upgradeability but removes the security mechanism, e.g. by replacing
 * `UUPSUpgradeable` with a custom implementation of upgrades.
 *
 * The {_authorizeUpgrade} function must be overridden to include access restriction to the upgrade mechanism.
 */
abstract contract UUPSUpgradeable is Initializable, IERC1822Proxiable {

    // 👉 설명: 현재 컨트랙트의 주소를 저장하여, 호출이 프록시를 통해 이루어지는지 확인하는 데 사용됩니다.
    /// @custom:oz-upgrades-unsafe-allow state-variable-immutable
    address private immutable __self = address(this);

    /**
     * @dev The version of the upgrade interface of the contract. If this getter is missing, both `upgradeTo(address)`
     * and `upgradeToAndCall(address,bytes)` are present, and `upgradeTo` must be used if no function should be called,
     * while `upgradeToAndCall` will invoke the `receive` function if the second argument is the empty byte string.
     * If the getter returns `"5.0.0"`, only `upgradeToAndCall(address,bytes)` is present, and the second argument must
     * be the empty byte string if no function should be called, making it impossible to invoke the `receive` function
     * during an upgrade.
     */
    string public constant UPGRADE_INTERFACE_VERSION = "5.0.0";

    /**
     * @dev The call is from an unauthorized context.
     */
    error UUPSUnauthorizedCallContext();


    // 👉 설명: 지원되지 않는 UUID 슬롯에서 발생하는 오류입니다.
    /**
     * @dev The storage `slot` is unsupported as a UUID.
     */
    error UUPSUnsupportedProxiableUUID(bytes32 slot);
    // 👉 설명: 호출이 프록시를 통해 이루어지는지 확인합니다.
    /**
     * @dev Check that the execution is being performed through a delegatecall call and that the execution context is
     * a proxy contract with an implementation (as defined in ERC1967) pointing to self. This should only be the case
     * for UUPS and transparent proxies that are using the current contract as their implementation. Execution of a
     * function through ERC1167 minimal proxies (clones) would not normally pass this test, but is not guaranteed to
     * fail.
     */
    modifier onlyProxy() {
        _checkProxy();
        _;
    }
    // 👉 설명: 호출이 delegatecall을 통해 이루어지지 않는지 확인합니다.
    /**
     * @dev Check that the execution is not being performed through a delegate call. This allows a function to be
     * callable on the implementing contract but not through proxies.
     */
    modifier notDelegated() {
        _checkNotDelegated();
        _;
    }

    function __UUPSUpgradeable_init() internal onlyInitializing {
    }

    function __UUPSUpgradeable_init_unchained() internal onlyInitializing {
    }

    // 👉 설명: 구현의 스토리지 슬롯을 반환하여 업그레이드의 호환성을 검증합니다.
    /**
     * @dev Implementation of the ERC1822 {proxiableUUID} function. This returns the storage slot used by the
     * implementation. It is used to validate the implementation's compatibility when performing an upgrade.
     *
     * IMPORTANT: A proxy pointing at a proxiable contract should not be considered proxiable itself, because this risks
     * bricking a proxy that upgrades to it, by delegating to itself until out of gas. Thus it is critical that this
     * function revert if invoked through a proxy. This is guaranteed by the `notDelegated` modifier.
     */
    function proxiableUUID() external view virtual notDelegated returns (bytes32) {
        return ERC1967Utils.IMPLEMENTATION_SLOT;
    }


    // 👉 설명: 새로운 구현으로 업그레이드하고, 주어진 데이터로 함수를 호출합니다.
    // 👉 이벤트: 구업그레이드가 완료되면 `{Upgraded}` 이벤트가 발생합니다.
    /**
     * @dev Upgrade the implementation of the proxy to `newImplementation`, and subsequently execute the function call
     * encoded in `data`.
     *
     * Calls {_authorizeUpgrade}.
     *
     * Emits an {Upgraded} event.
     *
     * @custom:oz-upgrades-unsafe-allow-reachable delegatecall
     */
    function upgradeToAndCall(address newImplementation, bytes memory data) public payable virtual onlyProxy {
        _authorizeUpgrade(newImplementation);
        _upgradeToAndCallUUPS(newImplementation, data);
    }
    // 👉 설명: 호출이 프록시를 통해 이루어지는지 확인합니다.
    /**
     * @dev Reverts if the execution is not performed via delegatecall or the execution
     * context is not of a proxy with an ERC1967-compliant implementation pointing to self.
     * See {_onlyProxy}.
     */
    function _checkProxy() internal view virtual {
        if (
            address(this) == __self || // Must be called through delegatecall
            ERC1967Utils.getImplementation() != __self // Must be called through an active proxy
        ) {
            revert UUPSUnauthorizedCallContext();
        }
    }
    // 👉 설명: 호출이 delegatecall을 통해 이루어지지 않는지 확인합니다.
    /**
     * @dev Reverts if the execution is performed via delegatecall.
     * See {notDelegated}.
     */
    function _checkNotDelegated() internal view virtual {
        if (address(this) != __self) {
            // Must not be called through delegatecall
            revert UUPSUnauthorizedCallContext();
        }
    }
    // 👉 설명: 업그레이드 권한을 확인하는 함수로, 서브클래스에서 구현해야 합니다.
    /**
     * @dev Function that should revert when `msg.sender` is not authorized to upgrade the contract. Called by
     * {upgradeToAndCall}.
     *
     * Normally, this function will use an xref:access.adoc[access control] modifier such as {Ownable-onlyOwner}.
     *
     * ```solidity
     * function _authorizeUpgrade(address) internal onlyOwner {}
     * ```
     */
    function _authorizeUpgrade(address newImplementation) internal virtual;

    // 👉 설명: 새로운 구현으로 업그레이드하고, 추가적인 설정 호출을 수행합니다.
    /**
     * @dev Performs an implementation upgrade with a security check for UUPS proxies, and additional setup call.
     *
     * As a security check, {proxiableUUID} is invoked in the new implementation, and the return value
     * is expected to be the implementation slot in ERC1967.
     *
     * Emits an {IERC1967-Upgraded} event.
     */
    function _upgradeToAndCallUUPS(address newImplementation, bytes memory data) private {
        try IERC1822Proxiable(newImplementation).proxiableUUID() returns (bytes32 slot) {
            if (slot != ERC1967Utils.IMPLEMENTATION_SLOT) {
                revert UUPSUnsupportedProxiableUUID(slot);
            }
            ERC1967Utils.upgradeToAndCall(newImplementation, data);
        } catch {
            // The implementation is not UUPS
            revert ERC1967Utils.ERC1967InvalidImplementation(newImplementation);
        }
    }
}

```

### ⚙️ PILicenseTemplate 함수들중 필요해보이는거 가져오기

// solhint-disable-next-line max-line-length
"max-line-length" 규칙은 코드의 각 줄이 특정 길이를 초과하지 않도록 요구하는 규칙입니다. 이 주석이 있는 경우, 해당 줄은 이 규칙의 적용을 받지 않게 됩니다. 주로 긴 코드 줄이나 가독성을 위해 줄 바꿈을 하지 않고 유지하고 싶을 때 사용됩니다.

솔리디티 NatSpec
https://velog.io/@octo__/Solidity-NatSpec-Format

@custom:oz-upgrades-unsafe-allow state-variable-immutable 주석은 OpenZeppelin의 업그레이드 가능한 컨트랙트 시스템과 관련된 특별한 주석입니다.
이 주석의 역할:
OpenZeppelin의 업그레이드 플러그인에게 이 변수들이 의도적으로 immutable로 선언되었음을 알립니다
일반적으로 업그레이드 가능한 컨트랙트에서는 immutable 변수 사용이 안전하지 않지만, 이 경우는 예외적으로 허용한다는 것을 명시합니다

**registerLicenseTerms**

라이센스 약관 등록하는 함수

```solidity
 function registerLicenseTerms(PILTerms calldata terms) external nonReentrant returns (uint256 id) {
    // 👉 설명: 로열티 정책 검사
        if (
            terms.royaltyPolicy != address(0) &&
            !ROYALTY_MODULE.isWhitelistedRoyaltyPolicy(terms.royaltyPolicy) &&
            !ROYALTY_MODULE.isRegisteredExternalRoyaltyPolicy(terms.royaltyPolicy)
        ) {
            revert PILicenseTemplateErrors.PILicenseTemplate__RoyaltyPolicyNotWhitelisted();
        }
    // 👉 설명: 통화 토큰 검사
        if (terms.currency != address(0) && !ROYALTY_MODULE.isWhitelistedRoyaltyToken(terms.currency)) {
            revert PILicenseTemplateErrors.PILicenseTemplate__CurrencyTokenNotWhitelisted();
        }
    // 👉 설명: 로열티 정책과 통화 토큰의 관계 검사
        if (terms.royaltyPolicy != address(0) && terms.currency == address(0)) {
            revert PILicenseTemplateErrors.PILicenseTemplate__RoyaltyPolicyRequiresCurrencyToken();
        }

        _verifyCommercialUse(terms);    // 상업적 사용 조건 검증
        _verifyDerivatives(terms);      // 파생 작품 관련 조건 검증

    // 👉 설명: 라이선스 조건을 해시화
        bytes32 hashedLicense = keccak256(abi.encode(terms));
        PILicenseTemplateStorage storage $ = _getPILicenseTemplateStorage();
        // 이미 등록된 라이선스인지 확인
        id = $.hashedLicenseTerms[hashedLicense];
        // license id start from 1
        if (id != 0) {
            return id;
        }
        // 새로운 라이선스 등록
        id = ++$.licenseTermsCounter;
        $.licenseTerms[id] = terms;
        $.hashedLicenseTerms[hashedLicense] = id;
    // 👉 설명: 이벤트 발생
        emit LicenseTermsRegistered(id, address(this), abi.encode(terms));
    }
```
**exists**

약관이 기존에 존재하는지 확인

```solidity
   function exists(uint256 licenseTermsId) external view override returns (bool) {
        return _exists(licenseTermsId);
    }
```

GirlGroupMembershipCollectionTemplate의 기능을 좀 정리해보자

ERC-7201, ERC165

GirlGroupMembershipCollectionTemplate의 기능을 좀 정리해보자

ERC-7201, ERC165
````
