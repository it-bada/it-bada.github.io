---
title: "LLM에서 Long RoPE 이해하기"
description: ""
coverImage: "/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_0.png"
date: 2024-05-15 23:39
ogImage:
  url: /assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_0.png
tag: Tech
originalTitle: "Understanding Long RoPE in LLMs"
link: "https://medium.com/towards-data-science/understanding-long-rope-in-llms-29337dc7e4a9"
---

## 오늘 이 블로그 포스트에서는 성능 하락이 없는 상태에서 LLMs의 맥락 길이를 확장하기 위해 사용되는 Long RoPE 방법론에 대해 자세히 살펴볼 것입니다.

![이미지](/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_0.png)

최근 일반 대중도 일상생활에서 LLMs를 사용하기 시작했을 때, 장시간 대화를 나눌 때 중요한 문제가 하나 발생합니다. 몇 차례의 대화가 이루어진 후에는 LLM이 이전에 말했던 내용을 완전히 잊어버린 것처럼 보일 수 있습니다! 실제로는 각 대화의 줄이 LLM의 맥락으로 전달되는데, 이것은 모델에 대한 거대한 입력이라고 생각할 수 있습니다. 대화가 너무 길어져서 맥락을 벗어나면 일부 데이터를 제거해야 합니다.

이것은 고객 경험이 좋지 않을 뿐만 아니라, LLM이 합리적으로 처리할 수 있는 정보량을 제한합니다. 그 결과, LLM의 맥락을 점점 더 크게 확장하기 위한 작업이 계속되어왔습니다.

오늘의 글인 "LongRoPE: 2백만 토큰 이상의 LLM 컨텍스트 창 확장"은 바로 그것을 이루어 냈습니다.

![이미지](/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_1.png)

위 그래프를 보면, 다음 토큰을 얼마나 잘 예측하는지에 관련된 손실을 측정하는 난해도가 LongRoPE에 대해 낮게 유지되지만 다른 방법론에서 급증하는 것을 볼 수 있습니다.

이 화려한 결과가 어떻게 발견되었는지 자세히 알아보겠습니다.

# 문맥 길이와 위치 인코딩

![UnderstandingLongRoPEinLLMs_2.png](/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_2.png)

고수준에서 시작하여, 트랜스포머는 입력에 대해 두 가지 정보를 필요로합니다: 토큰 임베딩과 위치 인코딩입니다. 토큰 임베딩은 tiktoken과 같은 것들로, 각 토큰에 대해 고유한 키를 생성하기 위해 고정된 어휘 크기를 사용합니다. 모델은 훈련을 통해 각 토큰에 대한 쿼리와 값을 학습하여 정보를 활용하여 다음 토큰을 성공적으로 생성할 수 있습니다.

![UnderstandingLongRoPEinLLMs_3.png](/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_3.png)

에 위치 지정 정보가 더 필요합니다. 문장에서 토큰의 위치를 나타내기 위해서요. 위의 방정식은 위치 정보를 전달하는 가장 추상화된 관점을 보여줍니다. 우리는 토큰의 각 요소마다 1개의 함수와 2개의 단어 임베딩 벡터(Xm과 Xn)가 있습니다. 여기서 m과 n은 각 벡터가 가지는 차이 있는 차원을 나타냅니다.

한 가지 방법은 보통 각 토큰을 보고 새로운 벡터를 만들어서 위치가 완벽하게 고유하도록 하는 것입니다. 당연히 여기서의 트레이드오프는 모델이 훈련 데이터에서 유사성을 보기 어렵게 하여 성능을 저하시킨다는 것입니다.

두 번째 방법은 각 토큰당 다른 벡터와 유사성 요소를 가진 벡터를 만드는 것입니다. 이렇게하면 여전히 다른 상황과의 유사성에 대한 정보를 캡쳐할 수 있습니다. 그러나 이러한 벡터들간의 충돌을 발생시킬 수 있으므로 이 방법론에서 생기는 혼란이 있을 수 있습니다.

이러한 방법들의 최적의 조합을 어떻게 찾을 수 있을까요?

## 회전 위치 인코딩 (RoPE)

업계는 대부분 양쪽을 잘 결합하는 방법으로 RoPE에 집중해왔습니다. 수학적 내용에 너무 깊이 들어가지 않으려고 합니다. RoPE는 사인 함수를 사용하여 토큰에 위치 값을 할당합니다. 사인 함수는 반복적으로 설계되어 있기 때문에 일부 위치 값은 다른 값과 매우 유사할 수 있습니다. 그 결과, 유사한 항목들은 얼마나 유사한지를 나타내는 양적 값을 갖게 됩니다.

![rotation image](/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_4.png)

위의 방정식에서 보듯이, θ 값 주변을 도는 다양한 함수로 채워진 희소 행렬을 가지고 있습니다. 이는 모든 위치 인코딩이 관련되도록 유지하는 방법으로 값을 전달합니다.

The connection between these θ symbols is illustrated below:

![UnderstandingLongRoPEinLLMs_5](/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_5.png)

When it comes to context size, the key element in this equation is the number 10,000. In our efforts to construct larger contexts within finite number ranges, the value of 10,000 has proven to be a constraining factor - as there is a limit to the number of vectors that can be generated using this number as a base.

![UnderstandingLongRoPEinLLMs_6](/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_6.png)

## 롱 평면 이후 로프 확장하기

만약 더 큰 위치 부호값을 사용하여 새로운 모델을 제로부터 훈련시킬 수 있다면, 왜 많은 사람들이 그렇게 하지 않는지에는 몇 가지 이유가 있습니다. 첫째, 제로부터 훈련하는 데에는 엄청난 비용이 듭니다. 현재 세계에서 하니즈 몇 조직만이 그 만큼의 자원을 가지고 있기 때문에, 이 작업의 부담이 상당합니다. 둘째, 대규모 고품질의 긴 텍스트를 찾는 것이 매우 어렵습니다. 훈련에 산천 개 토큰이 필요하다 면 그 정도의 품질이 있는 긴 데이터를 그 규모로 찾는 것은 큰 도전입니다.

결국, 연구자들은 로프를 더 큰 세타로 확장하는 다양한 방법을 제시해 왔습니다.

첫 번째 방법은 선형 위치 보간(PI)입니다. 여기서, 가능한 위치의 수를 θ를 어떤 값 λ로 줄여 선형적으로 보간합니다. 아래의 식은 이전의 모든 세타를 연결하는 데 사용한 θ^(2/d) 식을 Beta로 나타낸 것입니다.

![UnderstandingLongRoPEinLLMs_7](/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_7.png)

While this works, the authors of the paper note that there is a crowding effect where some of the information ends up getting lost after the reduction.

The second method is YaRN (Yet another RoPE extensioN method) where we divide the RoPE Dimensions into 3 groups and assign a different linear factor to each of them. The basic idea is that tokens that appear frequently should not be altered (their λ := 1) and the ones that are less so are altered. From the graph below, we can see that this works well at expanding up to 128k context length. The issue at play here is determining the groupings. The groups are determined by people and thus there can be sub-optimal decisions made that reduce performance.

![UnderstandingLongRoPEinLLMs_8](/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_8.png)

따라서, YaRN과 Linear Projection(PI)은 모두 작동하지만 한계가 있어 발전이 제한된다. Long RoPE는 각 아이디어의 장점을 살려 그들을 잘 결합하는 방법을 찾아냈다.

# Long RoPE 2의 통찰

Long RoPE 연구자들은 이전 방법을 개선하기 위해 두 가지 핵심 아이디어를 도입할 것을 깨달았다: (1) 좋은 λ의 분포가 불규칙적이므로 올바른 답을 가정하는 것보다 λ를 찾는 것이 더 나은 방법이며 (2) 위치를 변경하지 말아야 하는 토큰들의 하위 집합이 있다.

이러한 결과는 아래의 공식에서 찾을 수 있다. 최적의 λ를 찾기 위해, 손실 함수를 만들어 최소화할 수 있었다. 아래의 공식은 우리의 위치 벡터에 대한 스케일링을 나타내는 𝕀와 (n/βi)의 결과를 갖고 있다. 가장 작은 손실을 찾으면 해당하는 λ를 선택한다.

![Expansion Results](/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_9.png)

이 함수는 우리가 변경해서는 안 되는 토큰의 서브셋을 실현하는 방법입니다. 값 1을 선택함으로써, 거기에 위치 부호화를 그대로 유지해야 한다는 신호를 보내게 됩니다. 검색 범위를 제한하기 위해 '0, 1, 2, 4, 8, 12, 16, 20, 24, 28, 32, 64, 128, 256'의 n-hat 값을 고려했습니다. n-hat의 값이 더 높을수록, 원래의 위치 부호화를 유지하는 토큰이 늘어납니다.

# 확장 결과

이론적 부분을 다루었으니 이제 결과를 살펴봅시다!

![image](/assets/img/2024-05-15-UnderstandingLongRoPEinLLMs_10.png)

Long RoPE는 세부 조정 유무와 관계없이 작동합니다. 위의 그래프는 LongRoPE가 LLaMA2–7B에 적용되었을 때의 성능을 보여줍니다. 해당 모델의 초기 컨텍스트는 4천 토큰이었습니다. 최적의 λ를 찾아내어 그들은 놀랄만한 것으로는 32천 토큰까지 컨텍스트 창을 확장시킬 수 있었는데, 엔트로피 변동이 거의 없었습니다! 이것이 놀라운 점은 이와 같은 변경을 하기 위해 필요한 컴퓨팅이 세밀하게 조정하는 데 필요한 비용에 비하면 거의 무시될 만큼 작았다는 것입니다. 주요 컴퓨팅 비용 없이 8배 확장은 놀랍습니다.

큰 확장을 위해서는 세부 조정과 최적의 λ를 찾는 결합이 필요합니다. 논문의 연구자들은 이 방법을 따라 512배 확장을 이루었습니다. 먼저 모델 크기를 128천, 256천으로 증가시켰습니다. 128천에서 400 단계 동안 세부 조정한 다음 256천으로 추가 600 단계 동안 전환했습니다. 256천을 바로 세부 조정하는 것보다 더 나은 성능을 보였는데, 단순히 확장된 하나의 분포가 아니라 더 일반적인 분포를 학습함으로써 더 나은 성능을 얻을 수 있다는 것 같습니다. 그들은 최적의 λ를 다시 최적화하고 초기 4천 토큰 컨텍스트 창보다 512가 늘어난 2048천 토큰의 컨텍스트 창에 도달했습니다!

# 확장 이후 작은 컨텍스트 길이 처리하기

큰 맥락의 어려움 중 하나는 작은 맥락의 작업에 대한 성능 손실입니다. 이 동작은 이전에 관찰된 적이 있으며, 초기 데이터가 작은 범위로 압축되어 일부 주의력이 손실된다는 이론이 있습니다.

2048k 컨텍스트 창 모델에서는 더 짧은 길이에 대해 이상적인 λ를 찾아 문제를 해결했습니다 (논문에서는 4k 및 8k). 추론 중에, 만약 컨텍스트가 작다고 판단된다면, LLM은 위치 부호화 데이터에 작은 λ를 동적으로 사용하도록 전환합니다.

# 결론

LLM은 추론력에 뛰어나며, 현실 세계에서의 응용 프로그램으로 우리를 놀라게 합니다. 특히 제한된 비용으로 여전히 높은 성능을 유지할 수 있는 큰 컨텍스트 창이 있다면, 우리는 그 응용 분야가 계속 확장되는 것만 볼 것입니다.

한 가지 흥미로운 질문은 동적 위치 인코딩 계산이 미래의 방향이 될 수 있는가 하는 것입니다. 여러 위치 인코딩에서 세밀하게 조정하고 2λ의 품질 성능을 얻을 수 있다면, 추론 시간에 여러 λ 간을 매끄럽게 전환할 수 있는 1개의 모델이 있다는 것일지도 모릅니다.

LLM 공간에서 가장 흥미로운 점 중 하나는 데이터를 걸러내는 잠재력입니다. 인터넷은 정보에 대한 접근을 대중화하는 데 놀랄만한 일을 해왔지만, 우리의 삶을 불필요한 소음으로 넘쳐나게도 만들었습니다. 온라인에서 우리에게 거의 관련이 없는 것들이 많이 보여지고 있습니다. 평범하고 해로운 정보에서 중요한 정보를 추출해주는 도구가 있다면, 우리는 인터넷을 최대한 활용할 수 있을 것입니다.

더 넓은 맥락 창을 가지는 경우, LLM의 요약 및 정보 압축 능력은 더 큰 효과로 사용될 수 있습니다. 어쩌면 LLMs에게 두 가지 서로 다른 집합의 정보를 제공하고 그것을 각 집합의 전제에서 이성적으로 추론할 수 있는 새로운 것을 찾아내도록 하는 것에서 큰 발전이 올 수도 있습니다.

건설하는 것에 있어 흥미로운 시기입니다.

**자료 참고:**

- Ding, Y., 등. "LongRoPE: 2백만 토큰 이상의 LLM 컨텍스트 창 확장" (2024), arXiv
- Su, J., 등. "로포머: 회전 위치 임베딩이 포함된 향상된 트랜스포머" (2023), arXiv
- A. Vaswani, 등. "주의는 당신이 필요로 하는 전부" (2017), arXiv
- Peng, B., 등. "YaRN: 대규모 언어 모델의 효율적 컨텍스트 창 확장" (2023), arXiv
