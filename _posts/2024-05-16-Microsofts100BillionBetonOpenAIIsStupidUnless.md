---
title: "Microsoft의 OpenAI에 대한 1조 달러 투자는 어리석은 선택입니다 하지만"
description: ""
coverImage: "/assets/img/2024-05-16-Microsofts100BillionBetonOpenAIIsStupidUnless_0.png"
date: 2024-05-16 09:35
ogImage: 
  url: /assets/img/2024-05-16-Microsofts100BillionBetonOpenAIIsStupidUnless_0.png
tag: Tech
originalTitle: "Microsoft’s $100 Billion Bet on OpenAI Is Stupid. Unless…"
link: "https://medium.com/@ignacio.de.gregorio.noblejas/microsofts-100-billion-bet-on-openai-is-stupid-unless-5dc03d9c0ec9"
---


The Arizona desert houses a supercomputer created by a massive corporation to attain superintelligence - quite the science fiction plot, right? Well, it's happening now! Rumor has it that Microsoft is collaborating with OpenAI to establish the most advanced data center globally. They've even given this secret project a captivating name - Stargate.

The allocated resources for this endeavor seem mind-blowing, especially with the recent progress made in the AI realm aiming for a more streamlined future.



만약... 내가 단순사한 것일지도 모르죠. 장기 추론 인공지능 모델의 이론은 종이 위에 써져 있는 것이나, 세계 최고의 인공지능 연구소에서 더 나아가지 못한 것이 아니라 실제로 현실이 되고 있는 것일지도 모르는데, 우리 사회는 아직 이를 인식하거나 대비해두지 못해요.

# 역사상 가장 중요한 인공지능 법칙

시간이 흘러도 AI의 확장 법칙은 의심자들을 한없이 틀리게 증명해 왔습니다.

그리고 지금, 이 두 단어는 세계에서 가장 가치 있는 회사인 Microsoft를 이끌며 세계 66번째로 큰 경제의 GDP에 해당하는 투자를 단 한 프로젝트, 스타게이트에 집중하게 했어요.



But why, you might ask?

## Scaling: The First and Best Option

Even as Large Language Models (LLMs) are steadily approaching the trillion-parameter mark, with advanced models like GPT-4, Claude 3, or Gemini surpassing it effortlessly, we have yet to see any signs of saturation as models grow larger.

Simply put, creating larger models continues to deliver better results, plain and simple.



더 기술적인 용어로 말하자면, LLM이 커질수록 모델을 훈련하는 데 사용되는 매개변수는 계속해서 감소하고 있습니다.

모든 것을 고려해 봤을 때, 이러한 연구소 뒤에 있는 대규모 기술 기업들(구글, 마이크로소프트, 메타 등)은 점점 더 큰 데이터 센터를 구축할 만큼 강력한 인센티브를 가지고 있어야 합니다.

하지만 마이크로소프트가 다른 이유를 가질 수도 있습니다.

SemiAnalysis 블로그에서 설명한 대로, 구글의 컴퓨팅 능력은 다른 모든 사람들을 '어리석게' 만드는 수준이다.



위 이미지를 보실 수 있습니다.

하지만, 진실로 $100 억을 투자해야 할까요?

최근의 발전을 살펴보면, 분명히 그렇지 않습니다.



# 작아지는 경쟁

최근 연구 트렌드를 살펴보면, AI가 장기적으로 훨씬 저렴해져야 한다는 네 가지 중요한 발전 덕분에 저도 귀가 멀어진 듯합니다.

## 모든 것이 MoE

이제 어느 새 모델은 전문가들의 혼합(Mixture-of-Experts)이 아니면 없다고 볼 수 있을 정도입니다.



아름답게 설명된 하이에나 오퍼레이터의 논문에 따르면 "주목 메커니즘은 언어 처리를 위해 제곱 기능 중 작은 부분만 활용한다는 것을 보여주는 증거가 점점 더 늘어나고 있다."

다시 말해, 더 커지는 모델은 더 좋아지지만, 함수에 대해 근사하는 데 더 소홀해지며 매우 희소해진다는 것을 뜻합니다.

새로운 예측마다 모델의 매우 작은 부분만 실제로 예측에 참여하므로 매우 비효율적인 프로세스입니다.

그러므로 MoE는 매혹적인 기회를 제공합니다.



에는 전체 네트워크를 매번 실행하는 것은 돈과 시간 낭비라고 알고 있기 때문에 전문가(뉴런 그룹)로 모델을 '분할'합니다.

간단히 말해서, 아래에 표시된 대로, 각 예측마다 '루터'라고 불리는 소프트맥스 게이트가 일정 수의 전문가를 선택합니다.

이러한 전문가들은 이미 훈련 중에 존재하기 때문에, 이들 전문가 안의 뉴런들은 특정 주제에 특화되어 있습니다.

![이미지](/assets/img/2024-05-16-Microsofts100BillionBetonOpenAIIsStupidUnless_1.png)



그 방식으로, '모든 것을 아는' 하나의 거대한 신경망이 아닌, 매우 특정한 주제에 특화된 전문가 세트를 얻게 됩니다.

이에는 두 가지 의미가 있습니다:

- 각 예측마다 모델의 일부만 실행됩니다. 예를 들어, Mixtral 8x7B의 경우, 8명의 전문가 중에 각 예측마다 2명만 실행됩니다. 이는 450억 모델이 모든 예측마다 활성화되는 매개변수가 120억이라는 것을 의미하며, 비용이 4로 줄어들게 됩니다. 이는 큰 모델이 훨씬 작은 모델처럼 작동하는 것입니다.
- 보다 정확한 훈련. 각 뉴런 세트가 적은 주제를 배워야 하므로 그들의 지식을 요출하기가 더 쉽고, '지식 붕괴'의 가능성을 줄입니다.

하지만 모델들은 더 효율적으로만 되는 것이 아닙니다. 더 작아지고 있는 것입니다.



## 1-비트 시대

미국의 마이크로소프트가 주도하는 것은 놀랍게도 여기에 있습니다.

우리는 선도적인 예를 통해 각 매개 변수의 정밀도를 줄일 수 있지만 성능에는 눈에 띄지 않는 영향이 있다는 것을 깨닫고 있습니다.

게다가 모든 것을 1과 0으로 변환함으로써 행렬 곱셈을 필요로하는 것을 피할 수 있습니다. 왜냐하면 각 곱셈이 덧셈이 되기 때문입니다. 이것은 또한 GPU가 결국 그다지 필요하지 않을 수도 있다는 것을 의미할 것입니다.



![Image](/assets/img/2024-05-16-Microsofts100BillionBetonOpenAIIsStupidUnless_2.png)

But if this doesn’t seem convincing enough to you that the models are becoming more affordable, other researchers are also toying with the idea of challenging the established 'status quo' of the past 7 years in AI.

## Hybrid architectures, just a matter of time

Even though Transformers and their renowned attention mechanism boast top-tier performance, they are still not the perfect match for language tasks.



이유는 이 모델들은 비교할 수 없는 언어 모델링 성능을 제공하지만 엄청나게 비싸다는 것입니다.

문제는 무엇일까요?

음, Transformer는 상태가 없기 때문에 (반복적이고 고정된 메모리나 상태가 없음) 각 토큰은 시퀀스의 모든 다른 단어에 대해 자신이 주의를 기울이는 정도인 어텐션 점수를 계산해야 합니다. 이것은 어텐션의 비용 복잡성이 이차적이라는 것을 의미합니다.

이제 새로운 유형의 모델이 등장하고 있는데, 어텐션 연산을 버리지 않고 서브이차 연산과 결합시키는 방식입니다.



최근에 나온 좋은 예시가 있습니다. Mamba 연산자와 주의(그리고 전문가들의 혼합)를 결합한 Jamba는 독립형 트랜스포머의 성능을 맞먹으면서도 상당히 저렴하다는 것으로 나타났습니다.

그런데 혁신은 소프트웨어 쪽뿐만 아니라 하드웨어 수준에서도 일어나고 있습니다.

## 손에 반지를 꼽으세요

지난 몇 달 동안 가장 관련성 있는 혁신 중 하나는 Ring Attention입니다. 매우 낮은 메모리 요구 사항을 대폭 감소시키는 새로운 분산 컴퓨팅 아키텍처입니다.



사실, 여러 개의 GPU에 시퀀스를 분할함으로써 장치당 메모리 병목 현상을 없애고 엄청나게 긴 시퀀스 길이로 모델을 훈련하고 실행할 수 있게 됩니다.

그럼에도 불구하고, 거의 내일이 없는 것처럼 대규모 AI 기업들이 계속해서 GPU를 축적하고 있습니다. 그 이유는 바로 우리가 새로운 AI 패러다임으로 전환하고 있다는 사실 때문일 수도 있습니다.

하지만 이게 무슨 뜻일까요?

# 모델들에게 생각을 할 수 있게 해주세요!



지금은 너무나 압도적인 증거들이 있는 시기입니다. OpenAI부터 MIT, Google Deepmind에 이르기까지, 심지어 최근에는 Andrew Ng까지. 이유를 전적으로 이해할 수 없는 이유로, 모델이 탐색하고 반복할 수 있도록 추론 시간을 늘리면 결과가 현저히 향상된다는 점입니다.

아래에서 보시다시피, Agentic Workflows 내에서 실행될 때 심지어 GPT-3.5도 GPT-4를 압도합니다. 모델이 복잡한 작업을 해결하기 위해 당신처럼 반복할 수 있는 워크플로우에 포함되는 것입니다.

![이미지](/assets/img/2024-05-16-Microsofts100BillionBetonOpenAIIsStupidUnless_3.png)

그러나 이러한 모델과 프레임워크에는 문제가 있습니다.



그리고 그것을 증명하는 예시가 있습니다.

**경쟁 프로그래머와 수학 올림피아드 수상자**

작년이나 그 이후에 출시된 가장 인상적인 AI 모델 중 하나는 AlphaCode 2입니다. 이 모델은 Gemini 1.0 상에서 실행되는 AI 모델/프레임워크로, 경쟁 프로그래밍 대회에서 85% 백분위에 도달했습니다.

문제는 무엇일까요? 연구자들이 인정했듯이, 그것을 대규모로 배포하는 것은 단순히 너무 비용이 많이 든다는 것입니다.



이유는 명백하고 간단해요. 컴퓨팅 리소스를 엄청나게 많이 소비하죠. 문제 하나를 해결하려 할 때, 한 번에 그 문제를 해결하려는 대신 100만 개까지 다양한 가능한 답변을 샘플링해요.

그런 다음, 똑똑한 필터링, 클러스터링, 그리고 걸러내기를 통해 결국 하나의 답변을 선택하고 응답해요.

이 절차의 장점은 분명해요: 더 많은 샘플을 만들면, 올바른 답변을 발견할 확률이 높아져요.

Let. Models. Think.



또 다른 훌륭한 예는 Google Deepmind의 AlphaGeometry입니다. 여기서는 검색 알고리즘의 실제 구현을 볼 수 있습니다.

간단히 말해서, 이 모델은 '가능한 보조 구성물의 영역을 탐색'합니다 (기하학 정리를 간단히 하는 데 도움이 되는 단서). 이를 통해 연습문제를 좁히게 됩니다.

더욱이, 모델이 막다른 길에 처했을 때, 되돌아가 다른 경로를 탐색할 수 있습니다. 이는 올바른 경로를 탐색하는 가능성을 크게 향상시킵니다. 이 모델은 일부 정리를 증명하는 더 스마트하고 간단한 방법을 찾아내는 것으로 밝혀졌습니다.

그렇다면, 이 모든 것이 Project Stargate와 무슨 관련이 있을까요?



예술 또는 창의성과 관련된 주제를 재미있고 흥미로운 관점에서 다루는 포스트입니다.


자료에 따르면 OpenAI도 유사한 모델과 협력하고 있다는 것이 잘 알려져 있습니다. Q* (Q-Star)라는 이름으로 알려진 이 모델은 수학에 능한 검색 및 생성 알고리즘입니다. 


모든 것이 동일한 원리로 이어집니다:

LLM은 요청의 복잡성과 관계없이 토큰 예측 당 동일한 연산 노력을 할당하는데, 이는 바람직하지 않다고 할 수 있습니다.


**얼음 봉우리의 끝**



나에게 있어서, 스타게이트는 우리가 중요한 것을 찾아가고 있다는 명백한 징후입니다. 마이크로소프트가 GPT-6이나 그들이 어찌됐든 만들 것이 "더 큰 GPT-4"에 불과하다면 OpenAI에 1000억 달러를 투자하지 않을 것입니다.

그리고 그것이 불충분한 기준의 문제인지 아닌지에 상관없이, 사실은 LLM(Large Language Models)은 이전 버전을 향상하는 능력이 포화되는 것으로 보입니다. 예를 들어, GPT-4 교육이 끝난 후 거의 두 년이 지난 시점에 출시된 Claude 3는 약간 더 나아진 것 뿐입니다.

하지만 당신은 어떻게 생각하시나요? 대기업들이 단지 돈이 넘치는 상태라서 아무 말 없이 컴퓨트 자원을 낭비하는 것이라고 생각하시나요, 아니면 그들이 세상의 나머지 사람들이 알지 못하는 것을 알고 있는 것일지도 모르겠네요?

내 생각으로는, 스타게이트의 목적은 AI 모델의 다음 세대인 Long-Inference 검색 + 생성을 훈련하는 것이라고 생각합니다.



그리고 당신의 이야기는요?