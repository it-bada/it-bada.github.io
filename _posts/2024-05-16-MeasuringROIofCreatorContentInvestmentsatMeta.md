---
title: "Meta의 창조자 콘텐츠 투자의 수익성을 측정하기"
description: ""
coverImage: "/assets/img/2024-05-16-MeasuringROIofCreatorContentInvestmentsatMeta_0.png"
date: 2024-05-17 00:00
ogImage: 
  url: /assets/img/2024-05-16-MeasuringROIofCreatorContentInvestmentsatMeta_0.png
tag: Tech
originalTitle: "Measuring ROI of Creator Content Investments at Meta"
link: "https://medium.com/@AnalyticsAtMeta/measuring-roi-of-creator-content-investments-at-meta-df4e20061100"
---


이미지 링크를 다음과 같이 변경해주세요.

```
![Image](/assets/img/2024-05-16-MeasuringROIofCreatorContentInvestmentsatMeta_0.png)
```

다녀오신 지난 수년 간 Meta는 페이스북과 인스타그램에서 창작자들이 수익을 창출할 수 있게 해주는 다채로운 프로그램과 제품들을 구축해왔습니다. Meta의 창작자 수익화 제품의 목표는 두 가지로 나눌 수 있습니다: 창작자들에게 경제적 기회를 제공하고 활기찬 콘텐츠 생태계를 통해 사용자들에게 가치를 전달하는 것입니다.

이러한 프로그램이 창작자들과 사용자들 양쪽에 가치를 제공하기 위해서는 Meta에게도 재무적으로 지속 가능해야 합니다. 우리는 이러한 프로그램의 지속가능성을 평가하기 위해 이러한 투자가 사용자들에게 어떤 추가 가치를 제공하며 Meta에게는 어떤 비용을 지불해야 하는지를 계산하여 투자대비수익률(ROI)을 산정합니다. 그런 다음, 이러한 프로그램을 서로 비교하고 다른 제품들과도 비교하여 사용자들에게 가치를 제공할 수 있는지 여부를 평가할 수 있습니다.

그 본질적으로, ROI 공식은 간단합니다:

<div class="content-ad"></div>

ROI = Return / 투자 — 1

진정한 도전은 그 적용에 있습니다. 이 노트는 메타가 다운스트림 사용자 가치를 측정하고 창조자 투자에 대한 ROI를 평가하는 방법을 보여줍니다.

# Engagement Bonus Program을 위한 ROI, 간단한 예시

예를 들어 Engagement Bonus 프로그램을 살펴보겠습니다. 이 프로젝트에서는 페이스북에서 창조자의 콘텐츠 성능에 따라 보상합니다. 결과적으로 창조자들은 사용자가 가치 있게 여기는 콘텐츠를 더 많이 생성하고, 그 결과 사용자들을 더 자주 페이스북으로 되돌아오게 합니다. 우리는 보상, 콘텐츠 생산, 사용자 참여의 이 순환을 수익화 플라이휠이라고 합니다.

<div class="content-ad"></div>

![Image](/assets/img/2024-05-16-MeasuringROIofCreatorContentInvestmentsatMeta_1.png)

When we view the monetization flywheel from the perspective of ROI, we can define Investment as the program payout, and Return as the additional downstream user engagement it generates.

Measuring the investment is relatively straightforward - it's the amount Meta pays creators within a specific timeframe. However, assessing the return presents us with two complex questions:

- How do we quantify user engagement in monetary terms to standardize the measurement unit for both return and investment?
- How can we determine the extent to which the payout directly influences user engagement?

<div class="content-ad"></div>

To address question (1), we've created a set of revenue-weighted engagement metrics that assign monetary values to user engagement based on how effectively it leads to long-term monetization. One example is revenue-weighted time spent (rTS), where we calculate the time spent by considering monetization efficiency. Each category is determined by users in specific age groups, countries, and platforms.

![Image](/assets/img/2024-05-16-MeasuringROIofCreatorContentInvestmentsatMeta_2.png)

For question (2), we conduct two experiments—one for users and one for creators—to evaluate each stage of the monetization flywheel:

- Content Production → User Engagement: This user-level experiment entails reducing the visibility of content from monetizing creators to a random group of users to measure the increase in engagement their content generates.

<div class="content-ad"></div>

- 왜 중요한가요? 모든 콘텐츠에는 같은 가치가 있는 것이 아니며, 다른 플랫폼 콘텐츠로 대체하기 어려운 것도 있습니다. 콘텐츠 강등 테스트는 플랫폼 생태계에 대한 창출자의 콘텐츠가 얼마나 가치 있는지, 다른 콘텐츠 인벤토리의 대체를 고려할 때 얼마나 증가된 사용자 가치를 생성하는지를 판단하는 데 도움이 됩니다.

2. 결제 → 콘텐츠 제작: 이 창작자 수준의 실험은 일부 창작자에게 모네타이제이션 제품에 대한 접근을 제한하여 이러한 제품이 창작자 행동에 어떠한 영향을 미치고 콘텐츠 제작에 어떠한 영향을 주는지 이해하는 데 도움이 됩니다.

- 왜 중요한가요? 모네타이제이션 프로그램이 없을 때 일부 창작자들은 여전히 콘텐츠를 생산할 수 있지만, 그 속도는 떨어질 수 있습니다. 따라서, 모네타이제이션을 통해 창작된 모든 콘텐츠를 단순히 보상에만 귀속시킬 수는 없습니다. 창작자 점령 실험을 통해 보상에 귀속된 전체 생산량이 얼마인지를 결정할 수 있습니다. 이 비율을 생산자 측 가산률로 참조합니다.

모네타이제이션에 직접적으로 귀속된 증가된 사용자 가치를 계산하려면 아래의 두 실험 결과를 결합해야 합니다:

<div class="content-ad"></div>

![Link](/assets/img/2024-05-16-MeasuringROIofCreatorContentInvestmentsatMeta_3.png)

모두를 함께 보면 기본적인 보너스 프로그램의 ROI가 어떻게 계산되는지 간단한 관점으로 정리하였습니다:

![Link](/assets/img/2024-05-16-MeasuringROIofCreatorContentInvestmentsatMeta_4.png)

# ROI 커버리지 확대하기

<div class="content-ad"></div>

간단한 공식에서 시작하여 ROI 공식을 더 발전시킬 수 있습니다. 이를 통해 수익 공유 광고 (Instream Ads, Overlay Reels Ads 등) 및 유저 결제 제품 (Stars, Subscriptions 등)과 같은 다양한 수익화 제품의 효과를 평가할 수 있습니다. 이는 주어진 투자의 다른 소스의 유입과 유출을 포함하는 정의를 확장함으로써 가능합니다.

![image](/assets/img/2024-05-16-MeasuringROIofCreatorContentInvestmentsatMeta_5.png)

- 수익 공유 광고 제품: 내용 증가로 인한 증가된 수익 참여뿐만 아니라 광고 제품은 광고 형식 자체의 모너타이제이션 효율 향상으로 직접적인 추가 수익을 발생시킵니다. 경우에 따라 추가적인 직접 수익이 유입의 상당 부분을 차지하며, 프로그램의 재무적 가용성에 중요한 역할을 합니다.
- Stars & Subscription: 이 제품들은 메타에서 자금을 지원하지 않고 사용자로부터 직접 지급됩니다. 이들 프로그램은 모든 프로그램에 대한 ROI 계산에서 직접 지불 이외의 다른 비용을 고려하는 중요성을 강조합니다. 이 비용에는 제품 개입으로 인한 잠재적 사용자 참여 손실, 그리고 고품질, 통합 초점 제품 개발 및 유지에 관련된 OpEx 비용이 포함됩니다.

# 제작자 수익화 제품을 넘어선 ROI 평가

<div class="content-ad"></div>

이몽타주화된 제품의 투자 수익률(ROI)을 고려할 때 Meta로부터 직접적인 투자가 이루어진 경우가 가장 직관적인 것으로 여겨질 수 있습니다. 그러나 사용자 가치를 달러로 환산하여 투자 성과를 측정하고 제품 및 프로그램의 개발 및 유지 비용을 반영하는 좀 더 포괄적인 ROI 버전을 활용하면 창작자 모네타이제이션을 넘어 다양한 투자의 성과를 평가할 수 있습니다. 그러나 ROI는 궁극적으로 제한 요소이며 목표가 아닌 것을 명심하는 것이 중요합니다. 궁극적인 목표는 장기적으로 지속 가능한 방식으로 사용자들에게 기쁨과 매료시키는 경험을 전달하는 것입니다.

저자: Anish Dubey, Hanh Nguyen, Igor Stephanov, Mary Thomas