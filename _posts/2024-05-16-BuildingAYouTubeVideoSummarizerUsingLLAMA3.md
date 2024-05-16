---
title: "LLAMA3를 사용하여 YouTube 비디오 요약 프로그램 만들기"
description: ""
coverImage: "/assets/img/2024-05-16-BuildingAYouTubeVideoSummarizerUsingLLAMA3_0.png"
date: 2024-05-16 09:34
ogImage: 
  url: /assets/img/2024-05-16-BuildingAYouTubeVideoSummarizerUsingLLAMA3_0.png
tag: Tech
originalTitle: "Building A YouTube Video Summarizer Using LLAMA3"
link: "https://medium.com/@curiositydeck/building-a-youtube-video-summarizer-using-llama3-3291bf633638"
---


최근에 LLAMA3에 관한 YouTube 비디오를 많이 시청하다가 YouTube에 유포된 다양한 응용 프로그램을 발견했습니다. 제 관심을 끈 응용 프로그램 중 하나는 YouTube 비디오 요약 도구였습니다. 이건 시간을 많이 절약할 수 있겠죠? 비디오 링크를 전달하면 몇 초 안에 내용을 학습할 수 있다니 말이죠. 오늘은 Lightning Studio, Ollama 및 LLAMA3를 사용하여 무료 YouTube 비디오 요약 도구를 만들어보려고 해요.

우선 무료인 lightning.ai에서 스튜디오를 설정하는 것으로 시작할 수 있어요. Lightning은 구글 코랩의 대안으로 생각할 수 있어요. 초보자에게는 매력적인 크레딧 기반 요금제와 더 많은 공간이 있죠. 이 데모에서는 무료 티어 CPU 시스템을 사용해 모델을 로드하고 있어요.

스튜디오를 설정하면 해당 설명서에 있는 명령어를 사용하여 스튜디오에 Ollama를 설치할 수 있어요. Ollama는 로컬 기기에서 오픈 소스 대형 언어 모델과 상호 작용하는 강력한 도구에요. 이는 '당신의 LLMS용 도커'로 생각할 수 있어요.



스튜디오에 Ollama를 설치하고 다른 터미널에서 `ollama serve` 명령을 사용하여 Ollama 세션을 시작할 수 있어요.

이제 phidata 저장소를 열고 llama3 및 다른 요구 사항을 설치하세요. Phidata는 LLMS에 유틸리티를 추가하는 데 사용되는 프레임워크로, 이 프레임워크는 LLMS에서의 기억과 지식을 가능하게 합니다.

요구 사항이 설치되면 내장된 streamlit 라이브러리를 사용하여 app.py 파일을 실행하여 웹 애플리케이션을 시작할 수 있어요.

웹 애플리케이션 안에서 원하는 YouTube 비디오 링크를 붙여넣을 수 있어요. 여러분의 비디오 요약 어시스턴트가 몇 초 안에 비디오 요약을 생성해줄 거에요.



**이 비디오 요약 AI를 사용하면 시간을 절약하고 문제 해결에 집중하며 새로운 기술을 효율적으로 학습할 수 있습니다.** 
**개발자이든지 지식 애호가이든, 이 도구는 게임 체인저입니다.**
**귀하의 업무 흐름에 통합할 것인지 댓글로 알려주세요.**