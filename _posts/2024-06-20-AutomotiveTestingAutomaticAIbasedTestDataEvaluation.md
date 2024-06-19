---
title: "자동차 시험 자동 인공지능 기반 테스트 데이터 평가"
description: ""
coverImage: "/assets/img/2024-06-20-AutomotiveTestingAutomaticAIbasedTestDataEvaluation_0.png"
date: 2024-06-20 06:51
ogImage: 
  url: /assets/img/2024-06-20-AutomotiveTestingAutomaticAIbasedTestDataEvaluation_0.png
tag: Tech
originalTitle: "Automotive Testing: Automatic AI based Test Data Evaluation"
link: "https://medium.com/itnext/automotive-testing-automatic-ai-based-test-data-evaluation-f41a1ae17cd4"
---


## F1 텔레메트리 데이터 예시: 비지도 학습으로 시계열 전처리하기

# TLDR

차량을 테스트할 때 많은 양의 시계열 데이터가 생성됩니다. AI 방법을 사용하여 이러한 데이터를 전처리하고 중요한 섹션을 자동으로 표시할 수 있습니다. 이는 지도 학습이나 훈련 레이블이 필요하지 않은 비지도 학습 방법을 사용하여 수행할 수 있습니다. 시계열 데이터를 유사성에 기반하여 분석하여 데이터를 구조화하고 사용자에게 대화형 시각화를 제공할 수 있습니다.

애니메이션에서는 Formula 1 레이스의 텔레메트리 데이터를 사용하여 이러한 유사성 기반 분석의 예시가 보여집니다. 각 완료된 랩 후, 이전 랩에서의 모든 데이터가 평가되며 RPM 프로필에 대한 유사성 맵을 기반으로 점수가 계산됩니다. 시간이 지남에 따라 패턴이 보이며, 이를 통해 이상 이벤트를 식별하고 그를 자세히 검토할 수 있는 정보를 얻을 수 있게 됩니다.

<div class="content-ad"></div>

# 소개: 자동차 시험에서의 도전

안전하고 편안한 차량을 개발하기 위해 테스트는 필수적입니다. 그러나 CAN-Bus로부터 생성된 측정 및 원격 측정 데이터, 그리고 센서 데이터와 오디오 녹음은 채널이 많고 측정 시간이 길고 다양한 시험 변형이 있기 때문에 매우 방대합니다. NVH(소음, 진동 및 단단함), 동력 전달계, E/E 통합(전기 및 전자 통합), ADAS(고급 운전자 지원 시스템) 또는 수동 안전과 같은 다양한 시험 절차로부터의 데이터를 효율적으로 평가하는 것이 신속한 차량 개발에 중요합니다.

# 자동차 시험을 위한 AI 솔루션

때로는 간단한 규칙 기반 방법만 사용하여 데이터를 자동으로 전처리하고 작업 부담을 줄일 수 있습니다. 하지만 보통은 비정상적인 사건을 찾기 위해 수동, 경험 기반 작업이 필요합니다. 이를 자동으로 전처리함으로써 시간을 단축할 수 있습니다. 시험 데이터 평가를 위한 두 가지 AI 접근 방식은 후보 사건을 찾아내고 그 중요도에 따라 정렬하는 데 구분될 수 있습니다:

<div class="content-ad"></div>

지도 학습 AI 방법: 이미 발생한 이벤트에 대한 레이블이 지정된 평가 데이터가 있는 경우, 해당 데이터에서 브레이크 괭이와 같은 특정 이벤트를 감지하기 위해 지도 학습 AI 방법을 훈련하는 것이 유용할 수 있습니다.

비지도 학습 AI 방법: 이러한 방법은 레이블링이나 훈련 없이 데이터를 구조화할 수 있습니다.

- 클러스터링: 비슷한 데이터 포인트가 클러스터로 그룹화됩니다. 이를 통해 예를 들어 각 클러스터의 몇 가지 대표적인 멤버만 검토하여 시간을 절약하는 등 데이터의 공통점을 효율적으로 활용할 수 있습니다.
- 차원 축소: UMAP과 같은 차원 축소 방법을 사용하여 고차원 데이터를 저차원 표현으로 투영할 수 있습니다. 예를 들어 시계열 데이터를 보간하고 UMAP을 사용하여 2D 이미지로 투영하여 시각적인 표현을 만들 수 있습니다. 지역적 및 전역적 구조가 최대한 보존됩니다.

# 자동차 테스트를 위한 차원 축소: F1 텔레메트리 예시

<div class="content-ad"></div>

차원 축소 과정은 몇 줄의 코드로 복제할 수 있어요:

먼저 환경을 설정해보세요: Jupyter Notebook을 시작하고 필요한 Python 패키지를 설치해주세요:

```markdown
!pip install fastf1 pandas umap-learn renumics-spotlight
```

다음 패키지들을 사용할 거에요:

<div class="content-ad"></div>

- FastF1: Python library for easy access to historical F1 data — including telemetry and race results.
- Pandas: Python library for data analysis.
- umap-learn: Python library for dimensionality reduction that projects high-dimensional data into low-dimensional representations while preserving local and global data structures.
- Renumics-Spotlight: Tool for interactive visualization of structured and unstructured data.

First, the race data is loaded using the FastF1 interface:

```python
import fastf1
session = fastf1.get_session(2023, "Montreal", "Race")
session.load(telemetry=True, laps=True)
```

Now, you can access each lap's data for every driver as a DataFrame. This includes various information.

<div class="content-ad"></div>

***운전자:*** 차량의 운전자  
***랩 번호:*** 현재 랩 번호  
***속도 (시계열):*** 속도  
***엑셀 (시계열):*** 엑셀 위치  
***브레이크 (시계열):*** 브레이크 사용  
***RPM (시계열):*** 엔진 속도  
***X (시계열):*** 트랙 상 차량 위치를 나타내는 X 좌표  
***Y (시계열):*** 트랙 상 차량 위치를 나타내는 Y 좌표  

그런 다음, 이 데이터는 처음에 다음과 같이 변환됩니다.  

```js
def dataframe_to_dict(df):
    """팬더스 DataFrame을 리스트의 딕셔너리로 변환합니다.
    열이 오직 하나의 고유한 값만을 가지는 경우, 스칼라로 변환됩니다."""
    result = {}
    for col in df.columns:
        unique_values = df[col].unique()
        result[col] = df[col].tolist() if len(unique_values) > 1 else unique_values[0]
    return result
```  

텔레메트리 및 일반 정보를 위해 개별적인 딕셔너리로 변환됩니다. 시계열은 리스트로 변환됩니다:

<div class="content-ad"></div>

```js
# 랩 정보 및 텔레메트리 로드 및 딕셔너리의 목록으로 텔레메트리 로드
df_laps_telemetry, laps = [], []
for _, lap in session.laps.iterlaps():
    df_laps_telemetry.append(lap.get_telemetry())
    laps.append(lap.to_dict())
```

이제 모든 딕셔너리를 사용하여 만들어진

```js
# 각 운전자의 각 랩당 하나의 행을 가진 새 DataFrame 만들기
import pandas as pd
data = [dataframe_to_dict(tele) | lap for lap, tele in zip(laps, df_laps_telemetry)]
df = pd.DataFrame(data)
```

대규모 DataFrame:```

<div class="content-ad"></div>

```js
+----+----------------------+----------+-------------+-----------------+--------------------+----------------+----------------------+---------------------+
|    | Date                 | Driver   |   LapNumber | Speed           | RPM                | Brake          | X                    | ...                  |
|----+----------------------+----------+-------------+-----------------+--------------------+----------------+----------------------+---------------------|
|  0 | [Timestamp('2023-06- | VER      |           1 | [0, 0, 0, ...]  | [9812, 9753, ... ] | [False, False, | [3299, 3300,  ...]   |                     |
|    | 18, ...]             |          |             |                 |                    | ...]           |                      |                     |
| 1  | [Timestamp('2023-06- | VER      |           2 | [278, 278, ...] | [11033, 11045,     | [False, False, | [3356, 3374,  ...]   |                     |
|    | 18, ...]             |          |             |                 | ...]               | ...]           |                      |                     |
| 2  | [Timestamp('2023-06- | VER      |           3 | [279, 280, ...] | [11008, 11007,     | [False, False, | [3356, 3376,  ...]   |                     |
|    | 18, ...]             |          |             |                 | ...]               | ...]           |                      |                     |
...
+----+----------------------+----------+-------------+-----------------+--------------------+----------------+----------------------+---------------------+
```

To simplify further analysis, the data series to be analyzed should all be interpolated to the same length:

```js
import numpy as np
def interpolate_column(values):
    """This function interpolates a list of values to a fixed length of 882."""
    x = np.linspace(0, 1, 882)
    xp = np.linspace(0, 1, len(values))
    return np.interp(x, xp, values)
```

<div class="content-ad"></div>

```markdown
이후에는 그들의 차원을 줄일 수 있습니다:

```python
import umap
import numpy as np
embeddings = np.stack(df["Speed_emb"].to_numpy())
reducer = umap.UMAP()
reduced_embedding = reducer.fit_transform(embeddings)
df["Speed_emb_umap"] = np.array(reduced_embedding).tolist()
```

결과는 적절한 시각화 도구를 사용하여 표시 및 탐색에 활용될 수 있습니다. 이 예시에서는 Renumics-Spotlight를 활용했습니다.
```

<div class="content-ad"></div>

```markdown
To start an interactive visualization of the DataFrame, use the following code:

![Interactive DataFrame Visualization](/assets/img/2024-06-20-AutomotiveTestingAutomaticAIbasedTestDataEvaluation_0.png)

In the table on the left, the DataFrame is displayed. You can use the “visible columns” button to control which columns are shown in the table. The similarity map is shown in the top right. Selected data points are displayed at the bottom, where the speed profile is plotted.
```

<div class="content-ad"></div>

# Extended Example Online

저희가 Hugging Face의 데모 공간에 만들어 놓은 다른 예시가 있습니다. 시계열뿐만 아니라 시각화된 트랙 레이아웃과 각각의 운전자를 위한 속도와 기어를 색으로 표시한 내용이 포함되어 있어요:

![Track Layout](/assets/img/2024-06-20-AutomotiveTestingAutomaticAIbasedTestDataEvaluation_1.png)

트랙 레이아웃의 시각화를 통해 레이스에서의 차량 데이터 분석이 더 쉬워졌어요. 속도와 기어의 색으로 표시된 것을 통해 트랙 상의 중요 지점과 운전자들의 다양한 전략을 식별할 수 있어요.

<div class="content-ad"></div>

# Summary

자동차 산업에서 테스트 데이터를 반자동으로 평가하는 인공지능 방법의 활용은 상당한 장점을 제공합니다. 군집화 및 차원 축소와 같은 감독되지 않은 학습 방법을 통해 대규모 시계열 데이터 세트의 효율적인 분석이 가능해지면서 자동으로 관련 섹션을 표시할 수 있습니다. 이는 이상 사건을 더 빨리 식별하고 개발 프로세스를 가속화하는 데 도움이 됩니다.

F1 텔레미트리 데이터의 예시는 차원 축소를 통해 테스트 데이터를 어떻게 구조화하고 시각적으로 처리할 수 있는지를 보여줍니다.

저는 구조화되지 않은 시계열 데이터의 상호 작용적 탐색을 위한 고급 소프트웨어 솔루션을 만드는 전문가입니다. 데이터를 분석하고 정보에 기반한 결정을 내리기 위해 강력한 시각화 도구를 사용하는 방법에 대해 쓰고 있습니다.

<div class="content-ad"></div>

# 참고 자료

- McInnes, L., Healy, J., & Melville, J. (2018). **UMAP**: Uniform Manifold Approximation and Projection for Dimension Reduction. arXiv.