---
title: "팸의 재치를 발휘하다 스타듀 밸리 대화로 AI 봇을 만들어본 경험"
description: ""
coverImage: "/assets/img/2024-05-16-UnleashingPamsWitHowICreatedanAIBotwithStardewValleyDialogue_0.png"
date: 2024-05-16 19:46
ogImage: 
  url: /assets/img/2024-05-16-UnleashingPamsWitHowICreatedanAIBotwithStardewValleyDialogue_0.png
tag: Tech
originalTitle: "Unleashing Pam’s Wit: How I Created an AI Bot with Stardew Valley Dialogue"
link: "https://medium.com/@Matt_R_Steele/unleashing-pams-wit-how-i-created-an-ai-bot-with-stardew-valley-dialogue-0f4efb487888"
---


![image](/assets/img/2024-05-16-UnleashingPamsWitHowICreatedanAIBotwithStardewValleyDialogue_0.png)

펠리칸 타운의 한적한 마을, 바람에 흔들리는 작물과 닭들이 행복하게 울고 있는 곳에서, 내 마음속에는 다른 종류의 프로젝트가 준비되고 있었습니다. 게임과 기술을 모두 사랑하는 나는 유니크한 무언가를 만들기 위한 여정을 떠났습니다. 바로 Pam이라는 Stardew Valley의 사랑받는 캐릭터 대사를 이용해 트윗을 작성할 수 있는 봇을 개발하는 여정이었습니다.

계속 읽기 전에 StardewPam을 팔로우해보는 걸 적극 추천하고, 아래 이야기의 컨텍스트를 제공해주기 위해 조금의 배경 이해를 해보세요.

![image](/assets/img/2024-05-16-UnleashingPamsWitHowICreatedanAIBotwithStardewValleyDialogue_1.png)

<div class="content-ad"></div>

## 봇 트레이닝: 팸의 매력 드러나다

이미 더 오피스에 관한 트윗을 하는 봇을 만들어 놓았기 때문에, 상상 속 아늑한 농장 게임의 사랑받는 캐릭터를 재현하는 건 쉬운 과정이었습니다.

팸의 활기찬 매력을 트윗 봇에 불어넣는 여정은 신중한 방식이 필요했는데요. 먼저 최신 Stardew Valley 1.6 패치에서 팸의 대사를 추출하는 것으로 출발했습니다.

- 데이터 추출. Stardew Valley를 위해 사용 가능한 모딩 툴을 활용하여 게임 파일에 접근하여 팸의 대화를 추출했습니다. 이 파일에는 사랑받는 버스 운전사인 팸의 대화, 재잔, 생각들이 풍부하게 담겨 있었습니다.
- 분류 및 편집. 대사를 추출한 후, 다음 단계는 방대한 텍스트들을 살펴보고 어떤 팸의 대사가 "트윗 형식"에 최적화되었는지를 결정하는 것이였습니다. 이 과정은 주의깊은 수동 선별을 필요로 했고, 대사들이 시스템 특정 문자 없이 포맷팅되었도록 보장했습니다.
- 파일 생성. 팸의 대화를 갖고 있게 된 저는 팸의 대사들을 체계적인 구조로 봇의 학습을 위한 파일로 세심하게 만들었습니다. 각 대사는 봇이 글쓰기 스타일의 문맥과 목적을 이해할 수 있도록 제공되었습니다.

<div class="content-ad"></div>

![tarot](/assets/img/2024-05-16-UnleashingPamsWitHowICreatedanAIBotwithStardewValleyDialogue_2.png)

- 오픈AI에 업로드합니다. 훈련 파일을 준비한 후, 오픈AI 플랫폼으로 이동하여 세밀한 조정 기능을 사용하여 맞춤형 모델을 생성하는 과정을 시작했습니다. 훈련 파일을 업로드하고 모델의 학습 과정을 최적화하기 위한 매개변수를 지정했습니다. 이를 통해 모델이 Pam의 독특한 언어적 특성을 능숙하게 모방할 수 있도록 보장했습니다.
- 모델 훈련. 훈련 파일이 업로드되면 오픈AI 플랫폼이 최신 기술을 사용하여 Pam의 대화를 분석하고 이해하는 과정을 시작했습니다. 이를 통해 모델의 이해력을 미세하게 조정하고 Pam의 위트와 매력을 정확하게 모방하는 능력을 갖출 수 있도록 했습니다.
- 검증 및 테스트. 훈련이 진행됨에 따라 모델의 성능을 평가하기 위해 간단한 테스트를 수행했습니다. 이는 샘플 프롬프트를 입력하고 응답의 일관성과 진정성을 평가하는 과정을 포함했습니다.
- 모델 배포. 훈련이 완료되면 맞춤형 모델이 배포 준비가 완료되어, Pam의 매료되는 성격을 장착하고 트위터 버스에 그녀의 매력을 펼칠 준비가 되어 있습니다.

데이터 추출, 정리 및 모델 훈련을 통해, 트윗 생성 봇은 게임과 기술의 융합을 증명하는 것으로 나타났습니다. 주의 깊게 설계된 각각의 트윗에서 Pam의 정신을 대변하게 되었습니다.

문의사항 있으시면 X로 연락주세요.