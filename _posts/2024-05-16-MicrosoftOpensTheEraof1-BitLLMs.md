---
title: "마이크로소프트가 1비트 LLM 시대를 열다"
description: ""
coverImage: "/assets/img/2024-05-16-MicrosoftOpensTheEraof1-BitLLMs_0.png"
date: 2024-05-16 19:43
ogImage: 
  url: /assets/img/2024-05-16-MicrosoftOpensTheEraof1-BitLLMs_0.png
tag: Tech
originalTitle: "Microsoft Opens The Era of 1-Bit LLMs"
link: "https://medium.com/@ignacio.de.gregorio.noblejas/microsoft-opens-the-era-of-1-bit-llms-9568bfc9073a"
---


사실대로 가자면, 숫자는 거짓말을 하지 않아요.

시장이 AI와 함께 호황을 맞이하는 반면, 그 효과가 가치로 올라가지 않음은 명백하며 회사 중 4% 미만이 AI를 이용해 상품과 서비스를 생산하고 있습니다.

더 나쁜 점은 일부 대기업은 AI를 채용하고 있지만, 미쳐버릴 만큼 높은 비용 때문에 소규모 기업들이 따라갈 수 없어 동시에 본래 복잡한 작업을 대중화시키고 경쟁력을 증진시키기 위해 고안된 기술이 거대한 불평등의 장비로 변하고 있다는 아이러니한 상황입니다.

하지만 상황이 곧 바뀔 수도 있습니다. Microsoft가 조용히 1.58비트 대형 언어 모델 (LLM)을 출시했는데, 16비트 버전과 성능은 비슷하지만 훨씬 값싼 가격으로 빠르게 작동합니다.

<div class="content-ad"></div>

마이크로소프트는 1비트 LLM 시대라고 부르고 있어요. 이에 너는 그 모든 순간을 사랑할 거야.

# 돈이 없으면 파티도 없어

연구 수준에서 인공 지능이 이루는 멋진 결과에도 불구하고, 현재로서는 경제적 문제, 환경 영향, 가치 부재 등의 여러 가지 질환으로 고통받고 있어요. 이는 기존 예측한 것과는 다른 모습으로 성장하는데 제동을 걸고 있어요.

## 수치들이 맞지 않아

<div class="content-ad"></div>

오늘날에도 기업들 사이에서의 AI 도입이 이중 자릿수에 미치지 못한 것으로 최근 국가경제연구국의 연구와 MIT의 발표로 입증되었습니다.

![이미지](/assets/img/2024-05-16-MicrosoftOpensTheEraof1-BitLLMs_0.png)

하지만 이 연구는 대기업과 나머지 기업 사이의 명확한 불균형을 보여주는 더 걱정스러운 신호를 보여줍니다.

상처를 주고 또 업무상의 평평함이 크기뿐만 아니라 업종, 심지어 지리적 위치와 관련된 것이라는 것도 밝혀졌습니다.

<div class="content-ad"></div>

Kristina McElheran from the University of Toronto put it best:

But that’s just the tip of the iceberg. The environmental impact is a major concern as well.

With the AI industry already accounting for about 1% of global emissions, as reported by the University of Massachusetts Amherst, and with AI workloads expected to surge in the coming years, it's clear we are facing a significant challenge.

In essence, unless we find a way to make AI more efficient, its benefits will remain mostly exclusive to large corporations. Meanwhile, the rest of us might end up creating entertaining but trivial projects, like AI-powered raps about Texas barbecue in the style of Shakespeare.

<div class="content-ad"></div>

그러나 ‘1 대 다’ 시대를 가져온 생성적 AI의 패러다임 변화로 인해 가치 창출의 기회는 여전히 맹렬합니다.

## 기초적인 패러다임

오늘날 AI의 성공을 설명하는 가장 큰 이유는 바로 기초 모델(FMs)입니다. 이러한 모델들은 다양한 하향 작업을 수행할 수 있는 모델들로, 거대한 기초 AI 모델을 만들어 이를 이용함으로써, 주로 일반화를 달성했습니다. 이는 이전에 Gartner에 따르면 AI가 90%의 실패율을 기록한 것과는 대조적으로, AI를 성공 확률이 높은 기술로 발전시키고 더 매력적인 수익으로 이끌었습니다.

<div class="content-ad"></div>

마침내, AI는 학습을 요구하지 않았는데, 중요한 (때로는 비공개) 데이터를 실시간으로 제공하여 모델을 각 사용 사례에 구축하는 것으로 충분했습니다. 이를 공식적으로 프롬프트 엔지니어링이라고 합니다.

하지만 우리의 가장 큰 성공은 동시에 우리의 가장 큰 짐이 됩니다.

## 돈에 묶인

Frontier AI 모델은 병렬화 능력을 갖는 것들로, GPU와 같이 매우 비싼 하드웨어가 필요합니다.

<div class="content-ad"></div>

GPU의 기본성을 감안해도, LLM과 이러한 하드웨어 간의 관계는 완벽하다고 할 수 없어요.

우선, 오늘날 대부분의 모델은 하나의 GPU에 맞지 않는 크기를 갖고 있어요. 현재 우리가 가장 좋은 GPU인 NVIDIA의 H100이나 Intel의 Gaudi 2도 각각 80GB와 96GB의 High-Memory Bandwidth(HBM)을 가지고 있답니다.

많다고 느껴질 수 있지만, 우리가 이야기하는 모델은 ChatGPT나 Gemini Ultra와 같이 극단적인 경우에는 테라바이트 크기 범위일 수 있어요.

그 결과, 우리는 FSDP와 같은 분산 컴퓨팅 방법을 사용하여 모델을 부분으로 분해해야 해요. 이 방법에서 모델의 레이어들은 그룹으로 구분되어 각각을 하나 또는 일련의 GPU에 할당하게 됩니다.

<div class="content-ad"></div>

FSDP는 분산 문제를 일부 해결하지만, GPU는 훈련과 추론 모두를 위해 계산을 공유해야 하므로 통신 오버헤드가 추가됩니다.

더욱 복잡한 문제는 GPU의 배치도 중요하다는 것입니다.

현재 가장 흥미로운 접근 방식은 Ring Attention이라고 합니다. 여기서 GPU는 개별 GPU의 계산과 GPU 간 통신 오버헤드를 겹쳐 전역 예측 시간이 작업 부하의 분산된 성격으로 제약받지 않도록 GPU를 고리 모양으로 배치합니다.

한편, Predibase와 같은 기업들은 여러 모델을 한 GPU에 저장할 수 있는 간단한 서버리스 프레임워크를 제공하여 비용을 크게 줄일 수 있고, Groq와 같은 기관들은 심각한 속도를 가진 언어 처리 장치(Language Processing Units, LPUs)를 제안함으로써 추론 작업에 GPU를 전혀 사용하지 말아야 한다고 주장하고 있습니다.

<div class="content-ad"></div>

그러나 어떤 방법을 선택하든 핵심 문제는 여전히 남아 있습니다. LLM(Large Language Models)는 이상적인 것보다 훨씬 더 크며, 이전의 혁신들은 대부분 대형 모델 크기를 처리하는 문제 중심으로 이루어져 있습니다.

그 이유로 메모리 요구 사항이 핵심 병목 현상이라는 점을 고려할 때, 요즘 매우 인기 있는 해결책 중 하나는 모델을 양자화하는 것입니다.

그리고 여기서 이제, 마이크로소프트의 1비트 LLM이 등장합니다.

# 세상을 바꿀 1.58비트

<div class="content-ad"></div>

First of all, let's delve into the mysterious realm of quantization! 🌟

## Understanding Precision

Quantization is like the art of simplifying things. It involves reducing the level of detail or precision used to store the parameters (weights) of a model. This helps shrink the model's size and save memory, which is crucial for these complex models we've been exploring.

Typically, large language models (LLMs) employ 16-bit precision during training, where each weight is stored using exactly 2 bytes of memory. It's all about balancing accuracy with efficiency! 🌙

<div class="content-ad"></div>

다양한 방법들이 있지만 핵심 개념은 항상 같습니다. 무게의 값을 작은 비트 크기로 압축하는 것이죠.

가장 흔한 방법 중 하나는 16비트 가중치를 4비트 값으로 변환하는 것입니다. 이 시점에서는 실제 영향이 불분명해 보일 수 있지만, 아래 예시를 따라 주시면 좋겠습니다.

만일 이미 훈련된 50억 개의 파라미터를 가진 LLM 모델(오늘날 기준으로는 꽤 작은 모델)이 있다면, 2바이트 정밀도에서는 모델이 100 기가바이트의 무게를 지닐 겁니다.

결국 모델을 저장하려면 적어도 두 대의 NVIDIA H100 GPU가 필요할 것입니다.

<div class="content-ad"></div>

**하지만** 만일 당신이 가중치를 4비트로 양자화한다면, 기억 요구 사항이 4분의 1로 줄어들게 되어 모델이 갑자기 '단지' 25GB이 되어 단일 GPU에 완벽히 맞게 됩니다.

그런데 이게 너무 놀라운데, 왜 항상 그렇게 하지 않는 걸까요?

## 훈련 후의 트레이드 오프

대부분의 양자화 절차는 오늘날 훈련 이후에 수행됩니다. 즉, 모델을 혼합 또는 전체 정밀도(2 또는 4바이트)로 훈련한 다음 모델을 양자화하는 것을 의미합니다.

<div class="content-ad"></div>

자체 프로시저만으로도 중요한 문제가 발생할 수 있는데, 그것은 성능에 상당한 영향을 끼칠 것입니다. 하지만 만약 모델을 양자화된 상태로부터 처음부터 훈련시킨다면 어떨까요? 이것이 마이크로소프트가 추진하고 있는 방향입니다. 그러나 이를 극단적으로 취급하게 될 수도 있죠.

## AI의 미래?

<div class="content-ad"></div>

간단히 말하자면, 마이크로소프트의 논문은 선형 계층의 각 가중치에 대한 메모리 할당을 16비트에서 1.58비트로 줄여 매우 진보적인 방식을 제안합니다. 이는 메모리 요구 사항을 대략 16배로 줄이는 것을 의미합니다.

다시 말해, 선형 계층의 모든 가중치는 '1', '-1', 또는 '0'의 값을 갖습니다.

![image](/assets/img/2024-05-16-MicrosoftOpensTheEraof1-BitLLMs_1.png)

이렇게 함으로써, 일정 정밀도로 모델을 훈련한 다음 값들을 잘라내는 대신, 모델을 처음부터 양자화된 형태로 훈련시킬 수 있습니다.

<div class="content-ad"></div>

또 하나 주목할 만한 점은 이러한 가중치를 +/- 1 또는 0으로 설정함으로써 행렬 곱셈을 회피할 수 있다는 것입니다.

그리고 우리가 예상하는 대조적으로, 이 타협은 성능에 영향을 미치지 않았습니다. 오히려 그 반대였죠.

## 속도는 증가했지만 품질은 저하되지 않았습니다

유사한 가중치 수를 갖는 모델들과 비교했을 때, 이 모델은 우수한 성능을 보이며 대부분의 평가에서 상대 모델을 능가합니다.

<div class="content-ad"></div>

![Research](/assets/img/2024-05-16-MicrosoftOpensTheEraof1-BitLLMs_2.png)

연구자들은 이 방법의 주요 이점이 다른 크기에도 적용되며 규모가 커질수록 더욱 명확해진다고 주장합니다. 이는 다음을 의미합니다:
- "13B BitNet b1.58은 3B FP16 LLM보다 대기 시간, 메모리 사용량 및 에너지 소비 측면에서 더 효율적입니다."
- "30B BitNet b1.58은 7B FP16 LLM보다 대기 시간, 메모리 사용량 및 에너지 소비 측면에서 더 효율적입니다."
- "70B BitNet b1.58은 13B FP16 LLM보다 대기 시간, 메모리 사용량 및 에너지 소비 측면에서 더 효율적입니다."

큐얀티제이션-인식 트레이닝은 자체적인 스케일링 법칙을 개발함을 알 수 있습니다. 모델이 클수록 영향이 커진다는 것입니다.

<div class="content-ad"></div>

그리고 동일한 사이즈를 비교할 때 양자화된 LLM은 배치 사이즈를 11배 더 크게 만들어줍니다 (모델에 보낼 수 있는 개별 시퀀스 수), 초당 토큰 생성량이 9배 증가합니다.

![이미지](/assets/img/2024-05-16-MicrosoftOpensTheEraof1-BitLLMs_3.png)

그런데 이 모든 것이 의미하는 바는 무엇일까요?

그렇다면 곧 1비트 LLM이 보편이 될 수 있고, 엄청난 비용과 거대한 데이터 센터가 필요했을 일들이 결국에는 소비자용 하드웨어나 심지어 여러분의 스마트폰에서 운영될 수 있게 되는 일이 올 수도 있습니다.

<div class="content-ad"></div>

예를 들어, iPhone에서 실행할 수 있는 +100 억 개 파라미터 모델이 있을 수도 있고, 최신 노트북의 경우 +300 개 이상의 모델이 실행될 수 있습니다 (물론 대부분의 고급 소비자용 하드웨어에 이미 필요한 GPU가 있는 경우입니다).

하지만 우리는 더 나아갈 수도 있습니다.

곧 여러 다른 LLM이 병렬로 실행되는 디지털 제품이나 스마트폰과 같은 것이 나올 수 있습니다. 각 LLM은 그 하류 작업에서 특화되어 있을 수 있으며, 이는 우리 삶 속에서 LLM이 더욱 보편화될 수도 있습니다.

이것이 AI 가치 창출의 본질을 대표한다고 말하지 않는다면, 제가 할 말이 없습니다.

<div class="content-ad"></div>

## AI에 대한 심판의 해

올해 초에 나는 2024년이 이러한 혁신에 대해 더 많이 말할 것이며 'GPT-27'보다는 덜 이야기할 것이라 예측했고, 이러한 연구는 그런 방향으로 우리를 이끌어줍니다.

그리고 앞으로의 우리가 아직 확신을 갖고 통제하고 정렬할 도구를 개발하지 못했다는 점을 고려할 때, 최고 AI 연구소에서 개발 중인 미래의 슈퍼 모델들을 신뢰할 수 있게 제어하고 정렬하는 도구를 개발하는 것에 대해 바라봐 주기를 희망해 봅시다.