---
title: "M1 맥북 프로에서 Meta Llama 3 8b 모델을 실행해주세요"
description: ""
coverImage: "/assets/img/2024-05-15-RunMetaLlama38bModelonyourM1MacbookPro_0.png"
date: 2024-05-15 23:37
ogImage: 
  url: /assets/img/2024-05-15-RunMetaLlama38bModelonyourM1MacbookPro_0.png
tag: Tech
originalTitle: "Run Meta Llama 3 8b Model on your M1 Macbook Pro"
link: "https://medium.com/@shadabshaukat/run-llama3-on-your-m1-pro-macbook-08388b4b98e1"
---


Let's deploy the new Meta Llama 3 8b parameters model on your M1 Pro MacBook using Ollama.

![Click here to see the image.](/assets/img/2024-05-15-RunMetaLlama38bModelonyourM1MacbookPro_0.png)

Ollama is a fantastic deployment platform designed to make deploying Open Source Large Language Models (LLM) a breeze.

It usually takes around 15-20 minutes to have everything set up and running smoothly on a humble M1 Pro MacBook with 16GB of memory.



대부분의 시간은 실제로 5GB의 추론 파일을 다운로드하는 데 사용됩니다. 모델 자체는 약 30초 만에 시작됩니다.

## 1. 'https://ollama.com/download/mac'으로 이동해주세요.

![이미지](/assets/img/2024-05-15-RunMetaLlama38bModelonyourM1MacbookPro_1.png)

Zip 파일을 다운로드하고 압축을 풉니다.



## 2. 올라마 애플리케이션을 열어주세요. 그 후 애플리케이션으로 이동해주세요.

![image](/assets/img/2024-05-15-RunMetaLlama38bModelonyourM1MacbookPro_2.png)

## 3. 터미널을 열고 다음과 같이 입력해주세요.

```js
ollama run llama3
```



그럼 이제 끝났어요! 다운로드 및 빌드가 완료되기까지는 네트워크 대역폭에 따라 약 15-20분이 소요됩니다.

![image](/assets/img/2024-05-15-RunMetaLlama38bModelonyourM1MacbookPro_3.png)

브라우저에서 http://localhost:11434/을 열어서 Ollama가 실행 중인지 확인해보세요. 화면에 "Ollama is running"이 표시된다면 정상적으로 작동 중입니다.

## 4. 이제 Ollama를 실행하고 추론 속도를 테스트해봅시다.



마침내, MacOS에서 Ollama를 빠르게 시작하고 중지할 수 있는 별칭 바로 가기를 추가해 봅시다.

```js
vim ~/.zshrc

#파일에 아래 두 줄 추가

alias ollama_stop='osascript -e "tell application \"Ollama\" to quit"'
alias ollama_start='ollama run llama3'

#새 세션을 열고 아래 명령어를 사용하여 Ollama 시작 및 중지

ollama_start
ollama_stop
```

## 5. Llama3 성능 평가

```js
git clone https://github.com/shadabshaukat/llm-benchmark.git

cd llm-benchmark

python3.11 -m venv venv

source venv/bin/activate

pip install -r requirements.txt

# Ollama가 실행 중인지 확인하세요 'ollama serve'

python benchmark.py - verbose - prompts "하늘이 파란 이유는 무엇인가요?" "Nvidia의 재무에 관한 보고서 작성"

----------------------------------------------------

평균 통계:

----------------------------------------------------
        dolphin-llama3:latest
         프롬프트 평가: 40.44 t/s
         응답: 30.13 t/s
         총합: 30.45 t/s

        통계:
         프롬프트 토큰: 25
         응답 토큰: 576
         모델 로드 시간: 0.00초
         프롬프트 평가 시간: 0.62초
         응답 시간: 19.12초
         총 시간: 19.75초
---------------------------------------------------- 
```



행복한 AI체험 되세요 :)