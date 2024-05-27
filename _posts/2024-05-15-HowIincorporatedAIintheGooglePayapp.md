---
title: "구글 페이 앱에 인공 지능을 어떻게 도입했는지 알아보자"
description: ""
coverImage: "/assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_0.png"
date: 2024-05-15 19:27
ogImage: 
  url: /assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_0.png
tag: Tech
originalTitle: "How I incorporated AI in the Google Pay app"
link: "https://medium.com/design-bootcamp/how-i-incorporated-ai-in-the-google-pay-app-a761b4aabbdb"
---


A few weeks ago, I attended a workshop on Generative AI and was amazed by the insights it offered on the current applications of Artificial Intelligence. This inspired me to explore how I could leverage this technology for maximum impact.

As I delved into potential applications, I had a realization about my own financial habits. I noticed that I've been spending recklessly without proper monitoring, especially since I linked my bank account to UPI. This lack of control is a common concern for many individuals. To address this issue, I am planning to integrate AI into the UPI app.

India has witnessed a significant increase in digital payment adoption, with the Unified Payments Interface (UPI) becoming a popular choice for millions. In the fiscal year 2024, India recorded approximately 131 billion UPI transactions.

With the growing popularity of UPI payments, there is a demand for innovative solutions to enhance user experience and provide better financial management tools.



# 문제의 배경.

과거에는 현금을 사용할 때 소비에 대해 더 많이 신중했던 사람들이 많았습니다. 그러나 UPI와 같은 디지털 결제 방식이 늘어나면서 이러한 인식이 줄어들었습니다. 물리적인 현금 거래와는 달리 UPI 거래는 종종 덜 영향력이 있다고 느껴져 자주 지출되는 경향이 있습니다. 이러한 행동의 변화가 UPI 거래량의 증가에 기여했습니다.

![이미지](/assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_0.png)

사용자들은 종종 많은 거래를 관리하는 데 어려움을 겪고, 지출을 추적하고 분류하는 데 어려움을 겪습니다. 또한 개인 맞춤형 통찰력과 안내가 부족해 금융 목표를 효과적으로 설정하고 달성하는 데 어려움이 있습니다.



UPI 사용자들이 어떻게 증가했나요?
 
UPI 거래량의 증가는 여러 가지 요인으로 측정될 수 있습니다. 2014년까지 인도 성인 가운데 은행 계좌를 가진 사람은 53%에 불과했습니다. 그러나 2021 재정연도를 기준으로 이 수치는 급격히 90%로 늘어났습니다. 이 증가는 정부의 Jan Dhan Yojana와 같은 제도를 통해 재정 포용을 촉진하는 노력들에 기인합니다. 이를 통해 거의 모든 인도인이 은행 계좌를 갖는 것이 가능해졌습니다. 디지털 결제를 위한 사용자 베이스의 확장은 UPI 거래의 성장에 기여했습니다.

또한, UPI가 제공하는 사용 편의성과 편리함으로 인해 거래가 더 간단해지고 넓은 대중에게 접근하기가 더 쉬워졌습니다. 청구서 결제부터 온라인 쇼핑까지 모든 것이 디지턈화되면서 더 많은 사람들이 거래에 UPI를 활용하고 있습니다.

Arxiv의 조사에 따르면, UPI 사용자 중 81.10%가 매일 UPI를 사용한다고 합니다. 이는 평균적으로 UPI 사용자가 한 달에 30회 이상의 UPI 거래를 한다는 것을 보여줍니다. 응답자 중 UPI 앱의 사용자 베이스는 51.6%가 학생, 42%가 직장인, 4.7%가 사업가로 식별되었습니다. 성별 분포에 대해서는, 77%가 남성, 19.7%가 여성이었으며, 3.3%가 성별을 공개하고 싶지 않았습니다.



# 타로 전문가입니다. 지금 당신이 마주한 여러 가지 어려움들에 대해 이야기해주세요.

![마주한 문제들](/assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_1.png)

# 어떻게 해결할 수 있을까요?

앱을 위한 분석 페이지를 만드는 것은 이러한 문제를 해결할 수 있고 사용자들이 정보에 기반한 결정을 내릴 수 있게 도와줄 것입니다.



하지만 UPI의 사용자 기반을 고려해 볼 때, 인도에서 UPI를 사용하는 사람이 2억6천만 명이 넘기 때문에 모든 사람이 분석 페이지를 편안하게 사용할 수는 없을 것입니다.

그러므로 UPI 사용자 기반은 매우 광범위하며, 내 가설에 따르면 대규모 사용자 기반을 대상으로 디자인된 분석을 이해할 수 없는 사용자도 있을 수 있습니다. 교육적 배경이 부족한 사용자들은 광범위한 사용자 기반을 대상으로 디자인된 차트에서 통찰을 얻는 데 어려움을 겪을 수 있습니다. 교육적 배경을 갖춘 사용자는 쉽게 분석하고 추적할 수 있지만, 대규모 사용자 기반을 위해 디자인된 분석에서 더 개인화되고 고급 통찰 또는 예측을 얻기 어려울 수 있습니다.

그러므로 더 많은 사용자를 위해 해결책을 마련하고 다수의 사용자의 요구를 충족시키는 것이 옳은 선택이 될 것입니다.

Gemini AI를 활용하여 대화형 AI와 생성적 AI를 결합하면 사용자가 분석을 요청할 수 있으며, 개인화된 통찰과 권장 사항, 예산 편성 및 목표 설정에 대한 실시간 가이던스, UPI 거래를 통해 자신의 재정을 관리하는 데 개선된 전반적인 사용자 경험 등이 가능해집니다.



**Conversational AI**

Conversational AI는 인공지능을 사용하여 컴퓨터가 자연스럽게 인간 언어를 이해하고 대화식으로 응답할 수 있게 하는 기술을 말합니다. 이를 통해 사용자들이 AI와 대화하면서 소비 내역을 추적하고 재무를 관리하는 것이 더 편리해질 수 있습니다.

**Generative AI**

Generative AI는 사람이 생성할 수 있는 콘텐츠인 텍스트, 이미지 또는 오디오와 유사한 새로운 콘텐츠를 생성할 수 있는 인공지능 기술을 말합니다. 여기서 Generative AI는 소비 패턴을 분석하고 사용자의 질문에 답변하기 위해 통찰력, 제안이나 그래프를 생성할 수 있습니다.



# 내 사용자들은 이 기능을 이해하고 사용할 수 있을까요?

일상 어플리케이션에 AI 통합이 빠르게 증가하고 있어 사용자들을 고급 AI 기술에 적응시키고 있습니다. 그 중에는 아마존과 스포티파이가 성공적으로 생성 AI를 구현한 것이 있습니다. WhatsApp과 인스타그램은 메타 AI를 사용하고 있어 사용자들을 이러한 기술에 노출하고 있습니다.

또한, 이러한 도구들은 사용자 친화적이며 자명하며 채팅GPT를 대화형 AI에 수용하는 사용자들의 증가로 이러한 기능들을 이해해 가는 데 도움이 됩니다.

이러한 증가하는 친밀감과 적응력은 사용자들이 우리 UPI 어플의 생성 AI 기반 검색 기능을 이해하고 활용하여 사용자 경험을 향상시키는 유망한 요소로 기대됩니다.



# 이 기능이 비즈니스에 어떻게 도움이 될까요?

![이미지](/assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_2.png)

# 이 기능이 사용자들에게 어떻게 도움이 될까요?

![이미지](/assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_3.png)



## 솔루션에 대해 알아보기

사용자가 기능을 어떻게 발견하는지 알아봅시다.

![Google Pay의 AI 기능 활용](/assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_4.png)

Google Pay가 이 기능을 도입할 때 하단 시트가 표시되어 사용자가 이 새로운 기능을 쉽게 발견할 수 있도록 합니다.



이 사용자는 어떻게 검색을 통해 안내받게 될까요?

![이미지](/assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_6.png)

시스템이 검색에 실패할 경우에는 무엇이 발생할까요?



**How does this work?**

![Image 1](/assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_7.png)

**Personalise the results**

![Image 2](/assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_8.png)




- 간단한 방식: 사용자들이 기술 용어나 추가 정보 없이 간결하고 직접적인 답변을 받고 싶을 때 선택할 수 있는 옵션입니다. 사용자의 질문에 직접적인 답을 제공합니다.
- 그래프: 이 옵션을 선택하면 차트나 그래프와 같은 시각적 형식으로 정보가 제시되어 복잡한 데이터를 간편하게 이해할 수 있습니다.
- 자세한 내용: 사용자가 모든 관련 세부 정보와 맥락을 포함한 정보에 대한 포괄적이고 철저한 설명이나 분석을 원할 때 이 옵션을 선택할 수 있습니다.

# 지역 가맹점에 대한 결제를 어떻게 추적할 수 있을까요?

![이미지](/assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_10.png)



# 몇 가지 추가 예시 프롬프트

![HowIincorporatedAIintheGooglePayapp_11](/assets/img/2024-05-15-HowIincorporatedAIintheGooglePayapp_11.png)

# 몇 가지 검색 제한 사항

- 비텍스트 데이터: 검색 기능은 이미지나 비디오와 같은 비텍스트 데이터를 검색하는 것을 지원하지 않을 수 있습니다.
- 맥락 이해: 모호한 용어로부터 맥락을 이해하는 데 어려움을 겪을 수 있습니다.
- 제한된 역사적 데이터: 일정 기간 이전의 역사적 데이터에 대한 접근에 제한이 있을 수 있습니다.
- 개인정보 우려: 사용자의 개인정보 보호를 위해 민감한 정보를 검색하거나 접근하지 않을 수 있습니다.



# 향후 개선 사항

- 사용성 테스트를 실시하여 피드백을 수집하고 개선할 부분을 식별합니다.
- 음성 검색 기능 도입
- Google Pay 비즈니스(가맹점) 앱에 이 기능을 구현하는 데 초점을 맞춥니다.
- 보다 넓은 접근성을 위한 다국어 지원

# 결론

이 케이스 스터디를 통해 AI가 어떻게 응용되고 애플리케이션에 통합될 수 있는지, 특히 제품 디자이너로서 사용자에게 더 개인화되고 효율적인 솔루션을 제공하는 방법을 보여주고자 합니다. 다가오는 앱들은 유사한 AI 기술을 통합하여 사용자에게 더 발전된 사용자 친화적 기능을 제공할 가능성이 높습니다.



저는 구글 페이를 사용하여 이 기능을 시연했지만 이러한 기능은 폰페이, 페이티엠, 페이잽, 크레드 등의 다른 결제 앱에서도 구현할 수 있습니다.

이 케이스 스터디를 끝까지 읽어 주셔서 감사합니다.

만약 제 케이스 스터디가 마음에 드셨다면 👏🏻 하나 남겨 주시고 사랑을 보여주세요.

의견이나 피드백을 댓글로 공유해 주세요.



I love this vibrant energy you're bringing to the discussion! Let's connect through lakshmi.narayanan3002@gmail.com or on LinkedIn so we can dive deeper into the fascinating world of design together. I can't wait to hear your thoughts!