---
title: EP013 laya 흉내내서 snake game
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
tags:
  - AI
categories:
toc: true
toc_sticky: true
toc_label: 목차
description: desc가 여기에
---

작성일 : 2026.10.11

- Jev / Laya 스타일로 만듬


## 취지
- Jev/Laya 를 보고 비슷한 거 뭐 없나? 하고 찾아봄
- ModernBERT로 현재 좌표와 사과의 좌표를 주고, 상하좌우 다음 이동 위치를 받는 형태로 모델 구성 가능함을 알게 됨
- google colab에서 동작함 (GPU, CPU 둘다 사용해봄)
- GPU로 하면 좀 더 빠름, CPU로 해도 게임은 비슷한 속도로 가능

## ModernBERT 기반 스네이크 게임
- ModernBERT를 활용하여, 상하좌우 최적의 이동 방향을 판단하는 On-Device AI 자율주행 시스템.
- 이라고 쓰지만, 그냥 Gemini에게 해줘. 해줘. 해달라... 해줭... 을 반복해서 만듬.
  
### 1. 핵심 구동 원리

화면의 상황을 하나의 '문장(Text Prompt)'으로 임베딩한 후, 모델에 입력하여 가장 높은 확률을 가진 행동 카테고리를 추론(Inference)하는 다중 클래스 분류(Multi-Class Classification) 방식으로 작동.

데이터 파이프라인 워크플로우

```
[게임 환경 센싱] ➡️ [텍스트 프롬프트 변환] ➡️ [ModernBERT 인코더] ➡️ [Softmax 분류 헤드] ➡️ [최적 액션 결정]
  뱀/사과 좌표         "Context: Snake..."         토큰화 및 행렬 연산       [UP, DOWN, LEFT, RIGHT]       dx, dy 물리 제어
```

역시 이 설명도 너무 포장이 되었네.

### 2. 시스템 아키텍처 및 모델 구조

- 소프트웨어 구조는 Python 백엔드(딥러닝 추론 엔진)와 JavaScript 프론트엔드(60FPS 그래픽 GUI)가 구글 코랩(Google Colab) 환경에서 RPC(원격 프로시저 호출) 채널로 실시간 연동되는 하이브리드 아키텍처
- 네네.. 이것도 복붙의 연속, 해줘의 연속이었습니다.

```
┌─────────────────────────────────────────────────────────────────────────┐
│ 구글 코랩 가상 환경 (Google Colab Network Pipe)                         │
│                                                                         │
│  [Python 백엔드 엔진 Layer]                                             │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │  ModernBERT-base (Backbone) ➡️ 심층 특징 벡터 추출 (768차원)       │  │
│  └─────────────────────────────────┬─────────────────────────────────┘  │
│                                    ▼ (CLS Token Representation)        │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │  Decision Head (Linear ➡️ GELU ➡️ Dropout ➡️ Softmax Layer)       │  │
│  └─────────────────────────────────┬─────────────────────────────────┘  │
│                                    │  Inference Response (JSON)         │
│                                    ▼                                    │
│  [JavaScript 프론트엔드 GUI Layer]                                      │
│  ┌───────────────────────────────────────────────────────────────────┐  │
│  │  HTML5 Canvas 렌더링 ➡️ 실시간 텔레메트리 & Softmax 확률 바차트 출력 │  │
│  └───────────────────────────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────────────────────────────┘
```

### ① 입력 가공 (Feature Engineering & Tokenization)
매 프레임마다 뱀 머리의 좌표와 사과의 위치를 비정형 텍스트로 가공

```
Prompt 템플릿: "Context: Snake is at (10, 10) and Apple is at (10, 5) | Question: Which direction should snake move? | Choices: UP, DOWN, LEFT, RIGHT"
```
이 문장은 AutoTokenizer를 통해 정수형 토큰 ID 배열(input_ids)로 변환되어 모델에 인입

### ② 다운스트림 태스크 의사결정 헤드 (Decision Head)

ModernBERT 인코더의 최종 출력층에서 문맥의 총체적 의미를 담고 있는 [CLS] 토큰 가중치 벡터(768차원)를 추출
이를 커스텀 레이어에 통과시켜 최종 4개 선택지(UP, DOWN, LEFT, RIGHT)의 확률 점수를 계산
4. 프로젝트 결론 및 요약
NLP 기술 트랜스포머 임베딩 메커니즘을 정형 게임 루프에 적용

### Screenshot
<img width="507" height="687" alt="Image" src="https://github.com/user-attachments/assets/26c3acd7-d390-4543-9b06-b1388a307ccf" />

### 영상
<video controls width="640">
  <source src="https://github.com/user-attachments/assets/8e56d8fd-1864-4b6b-b2ce-5b15c1d5812b" type="video/webm">
    현재 브라우저에서 동영상을 재생할 수 없습니다.
</video>
