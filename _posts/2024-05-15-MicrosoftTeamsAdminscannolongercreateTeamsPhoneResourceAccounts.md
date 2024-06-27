---
title: "마이크로소프트 팀 관리자들은 더 이상 팀즈 전화 자원 계정을 생성할 수 없습니다"
description: ""
coverImage: "/assets/img/2024-05-15-MicrosoftTeamsAdminscannolongercreateTeamsPhoneResourceAccounts_0.png"
date: 2024-05-15 19:31
ogImage: 
  url: /assets/img/2024-05-15-MicrosoftTeamsAdminscannolongercreateTeamsPhoneResourceAccounts_0.png
tag: Tech
originalTitle: "Microsoft Teams Admins can no longer create Teams Phone Resource Accounts"
link: "https://medium.com/@easy365/microsoft-teams-admins-can-no-longer-create-teams-phone-resource-accounts-8a85431c6abf"
---


미국 서부에서 영업하는 한국 전자제품 수출입회사인 ABC Electronics에는 현재 아이온 아이폰 13와 같은 최신 스마트폰이 재고로 쌓여 있습니다. 이 중 몇 가지 제품을 할인 판매하기로 결정했습니다. 아래는 할인 대상 제품 목록입니다.

Markdown 형식을 사용하면 **이런 식으로** 텍스트를 강조할 수 있습니다. 여러분은 이 방법을 사용하여 제품을 소개하고 할인 혜택을 명확히 전달할 수 있습니다. 함께 즐거운 할인 이벤트를 즐기세요!



다양한 조직에서 이 변경은 팀 및 전화 관리자가 자원 계정을 설정하여 자동 응대기나 전화 대기열을 구축해야 하는 상황에서 중요한 역할을 합니다.

엔트라 관리자들과 팀/전화 관리자들 사이의 대립이 시작됩니다. 엔트라 관리자들은 최소한의 권한 원칙을 시행하려 하지만 팀/전화 관리자들은 자원 계정을 생성해야 하는 필요성을 느낍니다.

![이미지](/assets/img/2024-05-15-MicrosoftTeamsAdminscannolongercreateTeamsPhoneResourceAccounts_0.png)

# Microsoft가 왜 팀 자원 계정 생성을 위해 역할을 변경하는가요?



최근 몇 차례의 주목받는 사이버 공격 뒤에, 마이크로소프트가 보안 프로세스를 전면 개편 중인 것으로 보입니다. 이달 초, 마이크로소프트 CEO 사티아 나델라가 회사 내 20만 명 이상의 직원들에게 메모를 통해 보안을 최우선으로 두어야 한다는 것을 분명히 했죠.

나는 최근의 리소스 계정에 대한 변경 사항이 나델라가 발표한 새로운 지침을 따르는 마이크로소프트 보안팀의 결과라고 강한 의심을 품고 있습니다. 이 변경은 기존의 서비스 권한 사용을 중단하고 대신 Microsoft 365 관리자 역할의 권한을 사용하여 사용자 계정을 생성하도록 되어 있어요.

# 당신의 조직은 어떻게 준비해야 할까요?

지금은 팀 음성 관리자들이 리소스 계정을 생성하는 프로세스를 평가하고 필요한 권한을 부여할 사용자를 명확히하는 것이 필요합니다.



만약 팀 관리자에게 사용자 관리자 역할을 할당하려고 한다면, 몇 가지 고려해야 할 사항과 권장하는 방법이 있습니다.

글로벌 관리자와 사용자 관리자 역할은 둘 다 특권 있는 역할로, 다른 사용자에게 디렉터리 자원의 관리를 위임하거나 자격 증명, 인증 또는 권한 정책을 수정하거나 제한된 데이터에 접근할 수 있는 역할로 사용될 수 있음을 의미합니다.

요약하면, 특권 있는 역할 할당은 권한 상승으로 이어질 수 있으므로 사용자들에게 부여하는 것은 추가적인 주의가 필요한 중요한 책임입니다. Microsoft의 모범 사례는 조직 내 10 명 이하의 사람에게 특권을 제한하는 것을 권장합니다.

![Microsoft Teams Admins can no longer create Teams Phone Resource Accounts](/assets/img/2024-05-15-MicrosoftTeamsAdminscannolongercreateTeamsPhoneResourceAccounts_1.png)



# 특권 신원 관리(PIM)에서 타이트한 액세스 사용하기

PIM의 타임에스 액세스를 이용하면 글로벌 관리자나 특권 역할 관리자가 일부 Microsoft Teams 관리자에게 적격한 지정을 제공할 수 있습니다.

적격한 지정은 일시적인 액세스를 제공하며, 옵션으로 역할이 부여되기 전에 요청자가 비즈니스 사유를 제공하거나 지정된 결정자로부터 승인을 요청하는 등 추가 정보를 제공하도록 요구할 수 있습니다.

[마이크로소프트 팀 관리자가 더 이상 Microsoft Teams Phone 리소스 계정을 생성할 수 없는 문제](/assets/img/2024-05-15-MicrosoftTeamsAdminscannolongercreateTeamsPhoneResourceAccounts_2.png)



더 많은 정보를 원하시면 특권 ID 관리에서 Microsoft Entra 역할 설정을 구성하세요.

# API를 사용하여 Teams 전화 자원 계정 생성 자동화?

저와 같은 스크립터/앱 빌더들은 콜 대기열이나 자동 응대기의 대규모 빌드 아웃을 생성하는 동안 Teams Powershell 모듈이나 그래프에 대한 응용프로그램 기반 인증을 활용하여 리소스 계정을 생성할 수 없습니다.

![image](/assets/img/2024-05-15-MicrosoftTeamsAdminscannolongercreateTeamsPhoneResourceAccounts_3.png)



New-CsOnlineApplicationInstance 명령어는 사용자 계정과 대화식 로그인이 필요하므로, 추가로 사용자 관리자 역할이 필요할 것으로 보입니다. 그리고 아마도 글로벌 관리자 역할도 필요할 것입니다.

팀즈 파워쉘 모듈, Graph API 또는 기본 API가(Teams.PlatformService/ApplicationInstances) 그래프 역할 및 응용프로그램 기반 인증을 사용하여 팀즈 전화 리소스 계정을 생성하는 것을 허용할 수 있는 때를 고대하고 있습니다.

# 몇 가지 옵션이 있습니다

간단히 말해서, 이 변경으로 인해 팀 관리자들은 콜 큐 및 자동 응대기를 생성하는 방법을 다시 검토해야 할 것으로 보입니다. 가능한 대안은 다음과 같습니다:



- 새로운 Auto Attendants 또는 Call Queues를 만들 때 Teams Admins가 사용자 Admin 또는 Global Admin에게 리소스 계정을 요청할 수 있습니다.
- Just in Time Access를 사용하여 특권 Identities 관리(PIM)를 통해 Teams Admins에게 추가 역할을 부여하십시오.
- "대기 중"이며 할당할 수 있는 리소스 계정 풀을 생성하십시오. (Martin Heusser | M365 Apps & Services MVP님께서 그 아이디어를 나눠 주셨습니다)

다른 잠재적인 옵션/아이디어를 놓치지 않았는지요? 댓글로 알려주세요! 😊