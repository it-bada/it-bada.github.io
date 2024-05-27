---
title: "구글 IO 2024에서 개발자들을 위해 무엇이 준비되고 있는지 살펴봅시다 IDE와 Chrome에서의 Gemini, Firebase SQL 데이터베이스, Genkit, Project IDX, Kotlin Multiplatform, Checks, Agents에 주목할 예정입니다"
description: ""
coverImage: "/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_0.png"
date: 2024-05-17 22:25
ogImage: 
  url: /assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_0.png
tag: Tech
originalTitle: "What is coming for developers at Google I O 2024 — Gemini in IDEs and Chrome, Firebase SQL Database, Genkit, Project IDX, Kotlin Multiplatform, Checks, Agents"
link: "https://medium.com/@cengiztoru/google-i-o-2024-what-is-coming-for-developers-in-gemini-ides-and-chrome-sql-database-agents-8e8c44a7fb25"
---


우선, Rafah, Gaza, Palestine의 상황에 대해 매우 유감스럽게 생각합니다. 즉각적인 휴전을 요청하며 인도적 지원을 허용할 것을 촉구합니다. 팔레스타인은 진범에 벗어날 수 있기를 바랍니다.

# Gemini API & Google AI Studio

- Gemini 1.5 플래시는 이제 Google AI Studio에서 200개 이상의 국가와 영토에서 저지연으로 사용할 수 있습니다.
- Gemini의 장문 컨텍스트 기능을 통해 Figma 디자인과 같은 대규모 자료를 처리하고 이러한 디자인에서 프론트엔드 코드를 생성할 수 있습니다 (Locofy와 유사).
- Google AI Studio에 다양한 자료(시스템 지침, 블로그 글, 음성 메모)를 추가할 수 있습니다. 그런 다음 Google AI Studio에서 귀하의 프롬프트에 새로운 자료를 추가하여 Gemini에서 생성된 답변을 받을 수 있습니다. 예를 들어 블로그 글 생성하기 등.
- AI Studio의 Gemini API를 직접 앱에 통합할 수 있습니다.

<div class="content-ad"></div>

![Gemini Nano](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_1.png)

## 컨텍스트 캐시

프롬프트에 규칙적인 데이터(자료 참조와 같은)가 포함되어 있을 때 컨텍스트 캐시를 활용할 수 있어요. 이렇게 하면 비용을 절감할 수 있습니다. 이 자료에는 논문, 법적 문서, 학교 과제, 직원 교육 자료 등이 포함될 수 있어요.

# 지미니 나노

<div class="content-ad"></div>

**이미지 링크 생략**

- 장치 내 Generative AI 모델:
- 저렴한 대기 시간으로 장치에서 직접 실행되어 데이터와 개인 정보를 보호합니다. 메시징 앱에서 제안된 답변과 같은 기능을 가능하게 합니다.
- 또한, 이 기능은 이동 통신망이 없어도 작동합니다.
- 안드로이드의 핵심 부분이 될 전망입니다. Pixel 8 Pro 및 Samsung Galaxy S24 시리즈의 Gemini Nano 및 AICore와 함께 구비될 예정이며, 추가 장치가 이어서 출시될 예정입니다.
- 또한, MediaPipe를 사용하여 장치 내 ML 모델과 파이프라인을 만들 수 있습니다.

# 코틀린 Multiplatform 공식 지원 🚀

- Kotlin Multiplatform 지원은 Jetpack 라이브러리를 계속 추가할 예정입니다.
- Google 문서 앱은 안드로이드, iOS 및 웹 간에 비즈니스 로직을 공유하기 위해 KMP로 이전될 예정입니다. Gmail, 캘린더, 드라이브, Meet 등에 대한 미래 이전 계획이 있습니다.
- KMP는 플랫폼 간에 비즈니스 로직을 공유함으로써 생산성을 향상시킬 것으로 기대됩니다.

<div class="content-ad"></div>

# Android

![image 1](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_3.png)

- 콤포즈의 기능과 성능 개선이 지속되고 있으며 공유 요소 전환과 같은 기능이 추가되었습니다.
- 서로 다른 화면 크기에 대한 더 나은 반응성을 위해 새로운 레이아웃이 구현되었습니다

![image 2](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_4.png)

<div class="content-ad"></div>

- AI(인공지능) 기반 스타일러스 필기 인식 기술은 보기 및 작성 모두에서 필기를 텍스트로 변환합니다.

![Gemini in Android Studio](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_5.png)

위젯 빠른 시각, 크기 조정 가능한 에뮬레이터, 파이어베이스 장치

# 안드로이드 스튜디오의 지미니

<div class="content-ad"></div>

- 젬니(Gemini)는 Crashlytics 충돌을 분석하고 해결책을 제안할 것입니다.

![Gemini](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_6.png)

- 코드 변환, 문서 작성, 주석 등이 가능합니다. '다시 정제' 버튼으로 이전 프롬프트의 결과에 새로운 프롬프트를 추가할 수 있습니다.
- 변환 예시로는 코드 최적화, 코드 문서화, 문자열 번역, 테스트 작성 등이 있습니다.

## 🥳 😎 젬니 1.5 Pro의 멀티 모달 및 긴 문맥 기능을 사용하여 주어진 디자인으로 Jetpack Compose 화면을 구축할 수 있습니다.

<div class="content-ad"></div>

안녕하세요!
이미지 태그를 마크다운 형식으로 변경해 드렸어요.


![이미지](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_7.png)



![이미지](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_8.png)


올해 말에는 멀티 모달 기능이 제공되고, 변환과 정제 기능은 안드로이드 스튜디오의 코알라 버전에서 사용할 수 있어요.

프로젝트 게임페이스에 대해 더 알아보세요.
신랑디의 축복이 함께하기를 바래요! 🌟

<div class="content-ad"></div>

- 안드로이드를 위한 프로젝트 게임페이스가 출시되었습니다. 이 앱은 사용자들이 안드로이드 기기에서 머리 움직임과 표정을 통해 소설 커서를 제어할 수 있게 해줍니다. 이 프로젝트는 오픈 소스입니다.

![이미지](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_9.png)

# 웹

# 크롬의 제미니 나노

<div class="content-ad"></div>

- Chrome 126부터 Gemini가 Chrome 데스크톱 클라이언트에 탑재되어 온-디바이스 인공지능 사용이 가능해질 예정입니다.
- "Help Me Write"를 통해 사용자들은 제품 리뷰, 소셜 미디어 포스트, 고객 피드백 양식과 같은 짧은 형식의 콘텐츠를 온-디바이스 인공지능을 통해 작성할 수 있습니다. Google은 Gemini를 세밀하게 조정하고 Chrome에 최적화하여 이를 가능케 했습니다.
- 🚀 개발자로서, 프롬프트 엔지니어링, 세밀한 조정, 용량 또는 비용 프로세스 처리가 필요없이 고수준 API를 통해 Gemini의 기능에 액세스할 수 있습니다.

![Gemini 이미지](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_10.png)

- DevTools: Gemini는 사이트의 오류와 경고를 이해하며, Chrome DevTools 콘솔에서 문제를 이해하고 해결하는 데 도움이 되는 인사이트를 생성할 것입니다. 콘솔 인사이트는 현재 미국에서 실험적인 기능으로 제공되고 있으며, 곧 더 많은 국가에 롤아웃 될 예정입니다.

## Speculation Rules API

<div class="content-ad"></div>

![Image 1](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_11.png)

- Speculation Rules은 페이지를 미리 가져오고 백그라운드에서 페이지를 미리 렌더링하여 페이지가 밀리초 안에 로드되도록하여 웹 사이트의 속도를 향상시킬 것으로 예상됩니다. 이 API를 사용하려면 몇 줄의 코드만 필요합니다.

![Image 2](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_12.png)

## View Transitions API

<div class="content-ad"></div>

- **Chrome Canary 216**에서는 여러 페이지 앱에 대해 이전에 단일 페이지 앱으로 제한되었던 View Transitions API를 사용할 수 있습니다.

# 크로스 플랫폼

## 프로젝트 IDX

- **프로젝트 IDX**가 베타 버전으로 공개되었습니다. 이는 클라우드에서의 풀스택, 멀티플랫폼 앱 개발을 위한 AI 지원 워크스페이스입니다.
- 12개의 미리로드된 템플릿에 액세스할 수 있으며 기존의 GitHub 저장소를 가져올 수도 있습니다.

<div class="content-ad"></div>

![Image](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_13.png)

🌟 Hey there! Exciting updates from Google I/O 2024! 🌟

🔧 Dive into debugging Chrome Web apps with the powerful DevTools and Lighthouse features.

🌐 Explore the realms of multi-region deployment with Cloud Run—innovation at its peak!

🗺️ Enhance your apps with geo functionality effortlessly thanks to the Google Maps Platform enhancements.

### Checks Highlight:

- 💡 Simplify your app's privacy and compliance flow with Google's AI compliance platform, Checks.
- 🔍 Monitor code compliance in real-time and detect issues as you code for safer applications.
- 📱 iOS and Android developers now have access to Checks for a more streamlined development process.

Stay tuned for more updates and let your creativity soar! ✨

<div class="content-ad"></div>

![Image](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_14.png)

## 플러터

- WASM 지원이 오늘부터 안정 채널인 플러터 3.22 및 다트 3.4의 일부로 Flutter Web 앱에서 사용 가능합니다.
- 벤치마크에 따르면, Flutter 웹 앱을 WASM으로 컴파일하는 것은 JavaScript로 컴파일하는 Flutter 웹 앱에 비해 프레임 시간이 최대 2배 향상됩니다.

# 파이어베이스

<div class="content-ad"></div>

## SQL Database

- Firebase 데이터 연결과 Cloud SQL을 통해 Firebase에서 이제 SQL 데이터베이스를 사용할 수 있습니다. 현재 미리보기 단계입니다.
- 이를 통해 Firebase를 사용하여 보안 및 유형 안전한 앱을 구축하는 완전히 새로운 방법을 제공합니다.
- 쿼리는 자동으로 안전한 클라이언트 측 코드로 생성되어 앱 코드가 데이터 구조와 동기화되도록 보장합니다.
- Data Connect는 AI 개발을 위해 설계되었으며, 벡터 및 함수 호출을 지원하여 저장된 임베딩을 사용하여 AI 에이전트와 유사한 흐름을 생성하고 유사성을 찾을 수 있습니다.
- Data Connect를 테스트해보고 싶다면 미리보기에 등록하고 IDX의 원 클릭 템플릿을 탐색할 수 있습니다.

## Hosting

<div class="content-ad"></div>

- 현재 미리보기 중인 차세대 서버리스 호스팅 제품이 있습니다.
- App Hosting은 GitHub 저장소에서 소스 코드를 자동으로 가져 와서 프레임워크 빌드를 실행하고 필요한 구글 클라우드 인프라를 조정합니다.

## Firebase GenKit

- Firebase GenKit은 현재 베타 단계에 있는 오픈 소스 프레임워크로, 생산 준비 완료된 AI 기반 앱을 구축, 배포 및 모니터링하는 데 도움을 줍니다. 다양한 LLMs를 통해 API를 제공합니다.
- Gemini 및 Gemma를 지원하여 모델 변경이 쉽습니다.
- 지역 디버그 및 추적 지원이 포함되어 있어 Ollama와 Gemma를 사용하여 RTX GPU에서 GenKit을 로컬로 실행할 수 있습니다.
- GenKit을 사용하여 사용자 정의 콘텐츠를 생성하는 앱을 만들고, 의미론적 검색을 사용하며, 구조화되지 않은 입력을 처리하며, 비즈니스 데이터로 질문에 답변하며, 자율적으로 결정을 내리며, 도구 호출을 조정하고 등 다양한 기능을 사용할 수 있습니다!
- 현재 GenKit은 JavaScript/TypeScript(Node.js)로 서버 측 개발을 지원하고 있으며, Go 지원은 활발히 개발 중입니다.

![이미지](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_15.png)

<div class="content-ad"></div>

# AI 모델

![AI Models Image 1](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_16.png)

- Gemini 인프라를 기반으로 한 유연성과 제어성을 더욱 강화한 오픈 모델 Gemma 패밀리를 만들었습니다. 다양한 언어로 코딩 작업을 수행할 수 있는 CodeGemma입니다.
- 더 효율적인 메모리 사용 및 빠른 추론을 위해 반복 신경망 및 로컬 주의를 사용하는 RecurrentGemma입니다.
- 이미지에서 텍스트로의 다중 모달 변환 작업을 위한 PaliGemma입니다.
- Google AI Edge: 모바일, 웹 및 장치 애플리케이션용 장치 내 AI입니다.

![AI Models Image 2](/assets/img/2024-05-17-WhatiscomingfordevelopersatGoogleIO2024GeminiinIDEsandChromeFirebaseSQLDatabaseGenkitProjectIDXKotlinMultiplatformChecksAgents_17.png)

<div class="content-ad"></div>

## 데이터 과학 대리

- 제미니 1.5Pro와 그의 긴 문맥 기능을 활용하여 데이터셋을 업로드하고 관련 질문을 할 수 있습니다. 에이전트는 코드를 완성하고 계획을 구축하며 이를 실행하여 완전히 기능하는 Colab 노트북을 제작합니다. 지시사항에 따라 결과를 시각화하고 다른 사용자와 협업을 위해 이 노트북을 실시간으로 공유할 수 있습니다. 이 기능이 현재 사용 가능합니다.

# 구글 개발자 프로그램

- 프로그램의 구성원은 이제 새로운 혜택을 무료로 이용할 수 있습니다:
- 학습, 검색 및 문서와의 대화를 위해 제미니에 액세스할 수 있습니다.
- IDX 사용자의 경우, 두 대의 작업 스테이션에서 다섯 대로 이동할 수 있습니다.
- 구글 클라우드 혁신가 커뮤니티 구성원인 경우, 구글 클라우드 스킬 부스트의 인터랙티브 랩에 대한 크레딧을 받을 수 있습니다.
- 추가 혜택이 곧 출시됩니다.

<div class="content-ad"></div>

**미흡한 상황**

- 전기 자동차인 클래식 델로리안 자동차가 수상자에게 제공되는 이벤트가 있습니다.