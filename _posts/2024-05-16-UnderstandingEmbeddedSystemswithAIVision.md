---
title: "AI 비전을 이용한 임베디드 시스템 이해"
description: ""
coverImage: "/assets/img/2024-05-16-UnderstandingEmbeddedSystemswithAIVision_0.png"
date: 2024-05-16 23:59
ogImage: 
  url: /assets/img/2024-05-16-UnderstandingEmbeddedSystemswithAIVision_0.png
tag: Tech
originalTitle: "Understanding Embedded Systems with AI Vision"
link: "https://medium.com/@md.abir1203/understanding-embedded-systems-with-ai-vision-7fd1153f4ed9"
---


오늘은 또 다른 Large Language Models (LLMs)의 흥미로운 사용 사례를 살펴보겠습니다: 텍스트와 이미지를 모두 처리할 수 있는 AI 모델을 활용하여 임베디드 시스템을 이해하는 방법을 알아봅니다. LLMs가 어떻게 우리가 회로도를 더 빨리 해독하는 데 도움을 줄 수 있는지 살펴봅시다.

임베디드 시스템 회로도:

임베디드 시스템 회로도는 특별한 종류의 전자 시스템 안의 모든 부품과 선을 보여주는 지도와 같습니다. 엔지니어들이 모든 것이 어떻게 연결되어 있는지 볼 수 있도록 도와주며, 퍼즐을 맞추는 것처럼 작동합니다. 따라서 시스템을 설계하는 엔지니어이거나 시스템 작동 방식을 이해하려는 누군가라면, 이러한 회로도는 임베디드 시스템/마이크로컨트롤러의 의미를 이해하기 위한 안내서와 같습니다.

<div class="content-ad"></div>

**미리보기 시간:**

구글 제미니(Google Gemini)부터 시작해서 이전보다 빨리 임베디드 시스템의 도표를 읽는 데 이를 활용하는 방법을 살펴보겠습니다.

이어서 GPT-4의 유사한 프롬프트를 처리하는 능력에 대해 알아볼 것입니다.

<div class="content-ad"></div>

✨✨✨🔻🔻🔻🔻🔻🔻✨✨🔻🔻🔻🔻🔻🔻🔻✨🔻🔻🔻🔻✨✨🔻🔻✨🔻🔻🔻✨✨🔻🔻🔻

GPT-4가 잘 구조화된 결과물을 출력했어요. 그 비밀은 프롬프트에 있죠. 이어서 리뷰 섹션에서 보다 자세한 토론을 진행할 예정이에요.

이제 다른 비전 모델을 활용해 보는 시간이에요. 그것은 오픈소스입니다. 오픈소스란 컴퓨터에 대한 무료 "시력"이라고 할 수 있죠. 함께 오픈소스 비전 모델 LLaVA를 탐험해봐요.

![image](https://miro.medium.com/v2/resize:fit:1200/1*SRdmPRDiYFWwcwyhTNiv0g.gif)

<div class="content-ad"></div>

## 리뷰

상단의 3가지 비전 모델 출력을 통해 GPT-4와 Gemini이 유사한 답변을 제공하는 반면, LLaVA는 스키매틱 이미지의 이해 부족으로 판명되었습니다. 또한 Gemini는 검증을 위한 참고 자료를 제공했습니다.

비전 모델들에 대한 여러분의 경험을 댓글로 공유해 주세요!

#LLM #AI #Gemini #LLaVA #GPT-4 #VisionModels