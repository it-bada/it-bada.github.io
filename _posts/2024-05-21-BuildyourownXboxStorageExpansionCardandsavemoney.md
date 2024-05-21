---
title: "당신만의 Xbox 스토리지 확장 카드를 만들어 돈을 절안하세요"
description: ""
coverImage: "/assets/img/2024-05-21-BuildyourownXboxStorageExpansionCardandsavemoney_0.png"
date: 2024-05-21 00:12
ogImage: 
  url: /assets/img/2024-05-21-BuildyourownXboxStorageExpansionCardandsavemoney_0.png
tag: Tech
originalTitle: "Build your own Xbox Storage Expansion Card and save money"
link: "https://medium.com/@colton1070/build-your-own-xbox-storage-expansion-card-and-save-money-73fb2824ca20"
---


게임은 순환적이라고 느껴지는데요. 카트리지에서 디스크로, 하드 드라이브로 이어질 것 같았는데, 지금은 게임이 커져서 다시 카트리지로 돌아가는 것 같아요. 이 프로젝트를 시작할 때 제 생각이 그랬죠. Call of Duty HQ (240gb!)를 전용 저장 카드에 넣어서 공장 저장 용량을 다른 게임을 위해 보존할 수 있을까? 그럴 수도 있겠군요.

먼저, 저장 확장 카드가 무엇인지 알아볼까요? 이것은 Xbox가 Seagate 그리고 Western Digital에 라이선스를 부여하여 Xbox Series S|X 콘솔을 위해 제조한 외장 SSD입니다. 처음에 220달러에 출시된 Seagate 카드는 소비자 친화적이지 않았지만, 가격이 조금씩 내려오기 시작했어요. 나중에 Western Digital도 라이선스 버전을 150달러에 출시했는데, 이것 또한 Seagate 카드의 특징입니다. 이 카드들을 비싼 가격으로 만들어주는 요소가 무엇일까요?

Xbox의 벨로시티 아키텍처에 대한 등급이 NVMe SSD w/PCIe 4.0x2입니다. 콘솔 OS와 향상된 게임을 담고 있는 내부 SSD는 실제로 Western Digital SN530 NVMe SSD입니다. 인터넷에 찾아보면 찾을 수 있지만, 조금 기다려주세요! — 문제가 있어요. 콘솔에서 찾을 수 있는 것들은 CH로 표시되어 있지만 시장에 나온 제품은 PC로 표시돼요. 이 차이점과 레딧, 유튜브, 그리고 다른 곳에서 온 혼합된 보고들은 Xbox가 PC 타입 SSD를 인식하지 않을 것임을 경고했어요. CH 타입 SSD를 얻는 것은 여전히 가능하지만, 호환도 가능합니다 — CH 타입 SSD는 중고로만 찾을 수 있고 상용 저장 확장 카드와 비슷한 가격대에서 구할 수 있어요. 그래도 희망은 있습니다.

<div class="content-ad"></div>

이번 포스트에서 한 레딧 사용자가 PC SN530이 작동하지 않는 이유는 CH 버전이 SanDisk 컨트롤러를 통해 PCIe 4.0x2를 지원하도록 펌웨어가 조정되었기 때문이라고 주장했습니다. 그들의 생각은 시게이트 카드가 Phison E19 컨트롤러(PCIe 4.0x4)를 사용하기 때문에 호환되는 SSD와 CFExpress 어댑터를 찾으면 Xbox에서 사용할 수 있을 것이라는 것입니다. 저는 직접 연구를 하면서 그들의 포스트를 발견했고, 어떤 카드가 작동하고 어떤 것이 작동하지 않는지 이해하려고 했습니다. 그들은 "Sintech CFexpress to M.2 2230 Nvme 어댑터 카드, Xbox Series X/S Expansion Memory와 호환됨(Only Support WD CH SN530 /SSSTC XA1 PCIe4.0 SSD)"에 링크를 걸었습니다. XA1/XA2는 사실상 동일한 Prison E19 컨트롤러 사양을 충족하는 것입니다. 따라서 우리가 해야 할 일은 호환되는 SSSTC XA1 SSD를 찾는 것뿐입니다.

![Build your own Xbox Storage Expansion Card and save money](/assets/img/2024-05-21-BuildyourownXboxStorageExpansionCardandsavemoney_1.png)

이를 위해 70달러에 "보증 작동"하는 제품을 쉽게 찾았습니다. 불행하게도, 이 테스트를 위해 찾을 수 있는 가장 작은 크기는 1TB입니다 — 하지만 콜 오브 디티 본부가 얼마나 커질지 아무도 모릅니다, 맞죠? 저는 투자를 미래까지 대비하여 하고 있는 것뿐입니다. 우리가 필요한 마지막 것은 M.2에서 USB 리더기로, 카드를 컴퓨터에 쉽게 연결하여 새로운 저장 확장 카드로 사용할 준비를 하기 위함입니다.

요약하면 — 혹은 소개를 건너뛴 분들을 위해 요구사항은:
- 1TB 2230 M.2 SSD (PCIe 4.0x4) (이베이)
- XA1 to CFExpress Type B 어댑터 (아마존)
- M.2 to USB 어댑터 (아마존)
- 컴퓨터 (가능하면 윈도우)
- Xbox Series 콘솔 (당연히)

<div class="content-ad"></div>

자료를 모으면 M.2 SSD를 USB 어댑터에 넣어야 합니다. SSD를 어댑터에 맞게 길게 만들려면 SSD에 있는 길이 조절기를 사용하고 저장 카드 어댑터에 포함된 나사 중 하나를 사용하거나, 일단은 고무줄을 사용해 잡을 수 있습니다.

SSD/USB를 컴퓨터에 연결하고 windows 검색창에 diskpart를 입력하여 diskpart를 엽니다. 다음과 같은 콘솔이 열릴 것입니다.

![image](/assets/img/2024-05-21-BuildyourownXboxStorageExpansionCardandsavemoney_2.png)

다음 명령을 실행하세요:
list disk
컴퓨터에 연결된 디스크 목록이 표시됩니다. 일반적으로 SSD는 마지막 디스크일 것이지만, 포함된 메타데이터를 확인하여 SSD의 크기가 약 890GB로 표시됩니다. 번호로 "select disk #" 명령을 사용하여 디스크를 선택하세요. 바로 다음 단계가 디스크를 지우기 때문에 올바른 디스크를 선택했는지 확인하세요. 현재까지의 명령어를 이해하지 못하신다면 실행하지 마십시오.
그 다음, "disk clear" 명령을 실행하세요. 디스크가 지워졌다는 피드백을 받을 것입니다. 명령 프롬프트를 닫고 windows 검색으로 돌아가세요. "disk management"을 검색하여 디스크 관리 유틸리티인 "하드 디스크 파티션 만들기 및 포맷하기"를 엽니다. 거기서 "Disk X는 초기화되지 않았습니다."라는 팝업이 표시될 것입니다. SSD를 포맷하기 위해 안내에 따라 진행하세요. MBT가 선택되었는지 확인하세요. 초기화한 후, 초기화된 드라이브의 볼륨 영역 내에서 마우스 오른쪽 버튼을 클릭하여 새로운 간단한 볼륨을 만들어야 합니다. NTFS 형식으로 포맷하세요. 드라이브 문자와 볼륨 이름은 중요하지 않습니다. Xbox에서 다시 할당 및 이름이 지정될 것입니다.

<div class="content-ad"></div>

이 단계를 완료한 후 Xbox를 켜고 USB를 연결할 차례입니다. Xbox가 USB를 원격 저장공간으로 인식하지 못하기 때문에 우리는 Xbox USB 인터페이스를 통해 형식을 지정하지 않으면 되지 않습니다. 그리고 우리가 방금 한 단계 없이 USB 인터페이스가 그것을 인식하지 않을 것입니다.

Xbox에 연결한 후 저장장치에 대한 팝업이 표시될 것입니다. 저장 종류를 선택하라는 프롬프트가 나오면 Games and Apps를 선택하고 원하는 대로 이름을 지으십시오. Xbox가 드라이브 초기화를 완료하고 Xbox 저장 장치 페이지 (내 게임 및 앱 `관리` `저장 장치)에 나타날 것입니다.

이제 재미있는 부분입니다. 드라이브를 분리하고 USB 어댑터에서 빼내서 사용자 정의 확장 카드 케이스에 함께 넣을 수 있습니다. 어댑터에 포함된 열 패딩 필름을 제거하고 SSD의 칩 쪽에 부착하십시오. SSD를 저장 카드에 넣고 케이스에 나사로 고정하십시오. 제대로 조립하면 콘솔 뒷면에 연결하십시오. 진실의 순간 후 잠시 후에 다시 나타나서 게임을 다운로드할 수 있어야 합니다. 이제 $140이 드는 소매 버전 대신 약 $110에 게임 카트리지를 갖게 되었습니다. 네, $30은 많지 않지만 적어도 게임에 사용할 돈이 생겼습니다. 저장 용량이 작은 카트리지로 이 프로젝트를 다시 시도할 계획입니다. 가격을 카트리지 당 $50까지 낮추는 것이 목표입니다. 호환되는 것이 무엇인지 조사하고 알아내는 문제일 뿐입니다.

항상 그렇지만 문제가 발생하면 Google, Reddit을 사용하시고 여기에 의견을 남겨주시기 바랍니다. 도움이 필요하면 제가 도와드릴 수 있습니다. 행운을 빕니다. 그리고 즐거운 시간 보내세요.