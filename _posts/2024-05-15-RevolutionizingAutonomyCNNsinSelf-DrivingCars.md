---
title: "자율주행의 혁신 자율주행 자동차 속 CNN"
description: ""
coverImage: "/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_0.png"
date: 2024-05-15 12:20
ogImage: 
  url: /assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_0.png
tag: Tech
originalTitle: "Revolutionizing Autonomy: CNNs in Self-Driving Cars"
link: "https://medium.com/towards-artificial-intelligence/revolutionizing-autonomy-cnns-in-self-driving-cars-18c3ec446f5b"
---


## NVIDIA의 예측 주행 스티어링을 위한 DAVE-2 시스템 깊이 분석

![이미지](/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_0.png)

본 기사는 센터, 좌측, 우측 세 대의 카메라로부터 입력 이미지를 사용하여 주행 중인 자동차의 조향 휠 각도를 예측하는 데 합성곱 신경망(CNN) 접근 방식을 활용합니다. 사용된 모델 아키텍처는 NVIDIA가 자체 자율주행 시스템인 DAVE-2를 위해 개발했습니다. CNN은 Udacity 시뮬레이터에서 테스트되었습니다.

# 소개



자율 주행 자동차는 주변 환경을 감지하고 인간의 개입 없이 교통과 다른 장애물을 독립적으로 움직일 수 있습니다. (출처: [1]) 자율 주행 차량(AVs)의 사용은 거의 전 세계적으로 주요 산업이 되었습니다. 과거 몇 년 동안 보다 빠르고 가치 있는 차량이 생산되었지만, 더 많은 차량이 있는 가속화된 세계에서는 불행히도 사고 사례가 증가했습니다. 대부분의 경우 사고는 인간 운전자의 잘못이 원인입니다. 따라서 자율 주행 차량의 도움으로 이론상으로 대체 가능할 수 있습니다. (출처: [2]) Waymo, Zoox, NVIDIA, Continental, Uber와 같은 다수의 관련 기업이 이 제품을 개발 중에 있습니다. 이 종류의 차량을 통해 자동차 교통의 안전성, 보안성, 효율성이 향상되며, 운전이 가장 안전하게 이루어질 수 있습니다. (출처: [1])

AVs는 사람과 같이 주변 환경을 인식하고 수집한 정보를 기반으로 논리적인 결정을 내리기 위해 다양한 센서 기술에 의존합니다. 가장 일반적인 AV 센서 유형은 레이다, LiDAR, 초음파, 카메라, 글로벌 네비게이션 시스템 등이 있습니다. (출처: [3])

고급 운전자 보조 시스템(ADAS)은 다양한 자율 주행 수준을 분류하는 다계층 시스템입니다. 이는 완전히 인간 운전에서부터 완전히 자율 주행까지 다양한 수준을 보여줍니다. (Figure 1 참고)



# 합성곱 신경망 (CNNs)

현대 CNN에 대한 첫 연구는 1990년대에 발표되었으며, 네오코그니트론에 영감을 받았습니다. 야너 르쿤 등은 "Gradient-Based Learning Applied to Document Recognition" 논문에서 더 간단한 특징을 점차적으로 더 복잡한 특징으로 집계하는 CNN 모델이 손글씨 문자 인식에 성공적으로 사용될 수 있다는 것을 입증했습니다.

CNN은 하나 이상의 합성곱층을 가진 신경망으로 주로 이미지 처리, 분류, 분할 및 기타 자기 상관 데이터에 사용됩니다. CNN의 채택 이전에는 대부분의 패턴 인식 작업이 초기 특징 추출 단계에서 수동으로 수행되고 분류기가 뒤를 이었습니다. CNN의 발전으로 인해 훈련 예제로부터 특징이 자동으로 학습되어 인간의 성능을 훌륭하게 능가하는 것이 가능해졌습니다.

CNN 접근은 합성곱 연산이 2D 이미지를 캡처하기 때문에 이미지 인식 작업에서 매력적입니다. 또한, 전체 이미지를 스캔하는 데 합성곱 커널을 사용하면 학습할 매개변수가 총 연산 수에 비해 상대적으로 적기 때문에 효율적입니다.



# 데이터셋

데이터를 얻기 위해 Udacity 시뮬레이터 [6]에서 훈련 모드를 사용하여 차량을 수동으로 운전하여 첫 번째 트랙을 한 방향으로 4바퀴 돌고 반대 방향으로 4바퀴 더 돌았습니다. 데이터 로그는 CSV 파일에 저장되어 있으며 이미지의 경로, 폴더에 저장된 방향표, 스티어링 휠 각도, 액셀, 후진 및 속도를 포함하고 있습니다. 스티어링 각도는 1/25 배율로 사전 스케일링되어 있어 -1에서 1 사이의 값을 갖습니다. 제공된 데이터에는 6563개의 중앙, 왼쪽 및 오른쪽 jpg 이미지가 포함되어 총 19689개의 예시 데이터 크기가 있었습니다. 사진의 너비는 320이고 높이는 160이었습니다. 차량의 왼쪽/중앙/오른쪽 이미지 한 장을 찍은 예시는 아래와 같습니다.

![이미지](/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_2.png)

## 데이터 증강



확대는 데이터에서 가능한 많은 정보를 추출하는 데 도움이 됩니다. 모델이 훈련 중에 볼 이미지의 수를 늘리기 위해 네 가지 다른 확대 기술을 사용했으며, 이는 오버피팅 경향을 줄였습니다. 사용된 이미지 확대 기술은 다음과 같습니다:

- 밝기 감소: 밝기를 변경하여 낮과 밤 조건을 모방합니다.
- 좌우 카메라 이미지: 좌우 카메라 이미지를 사용하여 자동차가 측면으로 이탈하고 회복되는 효과를 모방합니다.
- 가로 및 세로 이동: 카메라 이미지를 가로로 이동시켜 도로 상의 자동차의 다양한 위치를 모방하고, 세로로 이동시켜 오르락내리락하는 효과를 모방합니다.
- 뒤집기: 훈련 데이터에서 좌우 회전이 균등하지 않기 때문에, 모델의 일반화를 위해 이미지 뒤집기가 필수적이었습니다.

다음 이미지는 적용된 데이터 확대의 예시를 보여줍니다.

![Data Augmentation](/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_3.png)



![Image 4](/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_4.png)

![Image 5](/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_5.png)

## 데이터 전처리

이미지를 증강한 후, 모델 훈련에서 사용하기 전에 데이터 전처리가 적용되었습니다. 전처리는 이미지 품질을 향상시켜 분석에 더 잘 사용할 수 있도록 합니다. 사용된 이미지 전처리 기술은 다음과 같이 설명됩니다:



- 잘라내기: 각 이미지의 하단 25픽셀과 상단 40픽셀을 잘라내어 차량의 전면과 지평선 위쪽의 하늘 대부분을 제거했습니다.
- RGB에서 YUV로 변환: 이미지를 RGB에서 YUV 유형으로 변환했는데, 이렇게 하는 것이 조명 변화와 모양 감지에 더 유리합니다.
- 크기 조정: NVIDIA 모델과 일관성 있게 유지하기 위해 모든 이미지를 66 x 200으로 크기 조정했습니다.
- 정규화: 이미지 픽셀 값에 255로 나누어 0과 1 사이의 픽셀 값만 남도록 했습니다.

아래 그림은 적용된 이미지 전처리의 예시를 보여줍니다.

![Image Preprocessing Example](/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_6.png)

## 데이터 생성자



수천 개의 새로운 훈련 인스턴스가 각 원본 이미지로부터 필요하기 때문에 이 모든 데이터를 디스크에 생성하고 저장하는 것은 불가능합니다. 따라서 Keras 제너레이터를 사용하여 로그 파일로부터 원본 데이터를 읽고 필요에 따라 데이터를 증가시키어 모델을 훈련하고, 각 배치에서 새 이미지를 생성했습니다.

## 모델 제안

이전에 언급했던 대로 CNN 모델을 사용했습니다. NVIDIA의 DAVE-2 시스템에서 사용된 모델에 영감을 받은 모델 아키텍처는 아래 그림 7에 나와 있습니다.

![Model Architecture](/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_7.png)



해당 모델은 다음과 같은 특징을 가지고 있어.

- 입력 이미지는 66 x 200 크기야.
- 5x5 필터를 사용한 세 개의 컨볼루션 레이어가 있는데, 신경망을 따라갈수록 각 레이어는 24, 36, 48의 깊이를 가지고 있어.
- 그런 다음, 3x3 필터를 사용한 두 개의 연속적인 컨볼루션 레이어가 깊이 64로 이어져.
- 결과는 완전 연결 단계에 들어가기 위해 평평하게 만들어져.
- 마지막으로, 점점 작아지는 완전 연결 레이어인 1164, 200, 50, 10이 순서대로 이어져.
- 출력 레이어는 하나의 크기이고, 이는 조향 각도 하나만을 예측하기 때문이야.
- 모델은 252219개의 학습 가능한 매개변수를 가지고 있어.

구현된 모델의 완전한 요약은 아래의 Figure 8에서 확인할 수 있어.

![Figure 8](/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_8.png)



모델은 활성화 함수로 지수 선형 단위(ELU) 비선형을 사용합니다. ReLU와는 달리 ELU는 음수 값을 가지며, 이는 평균 유닛 활성화를 제로에 가깝게 이동시킬 수 있도록 합니다. 아래 그림 9에서 ReLU와 ELU의 차이를 보실 수 있습니다.

![Figure 9](/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_9.png)

또한 Adam 옵티마이저가 사용되었는데, 이는 확률적 경사 하강법의 확장판으로 제곱 그래디언트를 사용하여 학습 속도를 조절하며, 훈련 데이터를 기반으로 네트워크 가중치를 반복적으로 업데이트합니다. 사용된 학습률은 0.0001 알파였습니다. 아래 표 1은 모델에 사용된 매개변수를 요약한 것입니다.

![Table 1](/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_10.png)



**카드 제작 및 검증**

이 모델은 NVIDIA GeForce RTX 3050 GPU를 사용하여 훈련되었고, 전체 훈련 소요 시간은 약 6시간이 소요되었습니다.

초기 데이터셋은 80%의 학습용 데이터와 20%의 검증용 데이터로 나뉘었습니다. 아래 그림 10은 학습과 검증 사이의 손실 비교를 나타냅니다.

![RevolutionizingAutonomyCNNsinSelf-DrivingCars_11](/assets/img/2024-05-15-RevolutionizingAutonomyCNNsinSelf-DrivingCars_11.png)



Figure 10 shows that as the epochs increase, the loss value decreases. At first, there's a noticeable gap between the training and validation loss, but they eventually converge to be almost the same.

The model underwent testing on two different tracks. While it performed adequately on the first track, where the training data originated, it showed instability with frequent small corrections between left and right.

In contrast, the model behaved much better on the second track, demonstrating consistent and excellent performance, indicating strong generalization capabilities.

You can watch the video showcasing the model's performance on both tracks through the following link: [Self-Driving Car: Predicting Steering Wheel Angle using Udacity’s Simulator — Model Performance](youtube.com)



# 결론

깊은 신경망과 다양한 데이터 증강 기술을 사용하여 차량의 조향 휠 각도를 신뢰할 수 있는 방법으로 예측하는 모델을 만들 수 있다는 것이 입증되었습니다.

결과를 관찰한 후, 얻은 모델은 두 트랙에서 모두 잘 수행했기 때문에 매우 좋습니다. 그러나 매개변수를 조정하고 에폭 수를 늘림으로써 더 나은 교육을 할 수 있습니다.

현재와 같은 성능을 내면서 더 짧은 교육 시간에 더 나은 모델을 만들기 위해 모델 매개변수를 조정할 수 있습니다.



미래에는 다른 모델 아키텍처를 사용해 성능을 탐색하거나 다양한 데이터 증강 기술을 적용하며 강화 학습 모델을 실험하고, 실제 자동차에서 모델의 성능을 테스트해보는 것도 좋을 것 같아요.

독자 여러분, 감사합니다!

# 참고 자료

[1] Manikandan, T. (2020). Self-driving car



## References:

- Szikora, P. (2017). *Self-driving cars — The human side*
- Vargas, J., et al. (2021). *An Overview of Autonomous Vehicles Sensors and Their Vulnerability to Weather Conditions*
- Draelos, R. (2019). *The History of Convolutional Neural Networks*
- Bojarski, M., et al. (2016). *End to End Learning for Self-Driving Cars*



[6] Udacity. (2016). Udacity’s Self-Driving Car Simulator.

[7] Yang, L., et al. (2020). Random Noise Attenuation Based on Residual Convolutional Neural Network in Seismic Datasets