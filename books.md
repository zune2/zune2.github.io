---
title: 머신러닝 / 딥러닝 / AI 엔지니어 로드맵
layout: single
permalink: /books/
author_profile: true
comments: false
toc: true
toc_sticky: true
toc_label: 목차
read_time: true
---

# 머신러닝 딥러닝 로드맵

## 📋 1단계: 데이터 분석 및 ML 수학 기초

1. NumPy로 고유값(Eigenvalue)과 고유벡터(Eigenvector)를 구하고 선형 변환 시각화하기
2. 합성함수의 미분을 위한 연쇄 법칙(Chain Rule)을 코드로 구현하여 경사 기울기 계산하기
3. 가설 검정(p-value)과 베이즈 정리(Bayes' Theorem) 개념을 활용한 데이터 추론 실습하기
4. SQL 복잡한 JOIN문과 Window 함수(RANK, LEAD, LAG)를 사용해 로우 데이터 정제하기
5. Pandas로 결측치(Null) 임퓨테이션 및 사분위수(IQR) 기준 이상치(Outlier) 제거하기
6. Seaborn의 pairplot과 heatmap을 활용하여 변수 간 상관관계 분석 및 EDA 보고서 작성하기

## 📋 2단계: 전통적 머신러닝 (Classical ML) 마스터

7. 수치형 특성에 StandardScaler를 적용하고, 범주형 특성에 One-Hot Encoding 파이프라인 구축하기
8. 데이터 누수(Data Leakage)를 방지하기 위해 K-Fold Cross Validation을 적용한 검증 환경 만들기
9. Linear Regression 모델을 학습시키고 규제(Lasso, Ridge)에 따른 가중치 변화 비교하기
10. Decision Tree 분류 모델을 만들고 과적합 방지를 위해 트리 깊이(Max Depth) 제한해 보기
11. XGBoost, LightGBM, CatBoost의 하이퍼파라미터를 Optuna 라이브러리로 자동 튜닝하기
12. K-Means 알고리즘으로 유저 군집화를 진행하고, PCA를 활용해 2차원 평면에 군집 결과 시각화하기
13. 불균형 데이터셋 분류 후 Confusion Matrix를 그리고 F1-score 및 ROC-AUC 곡선 평가하기

## 📋 3단계: 심층 신경망 및 딥러닝 기본 (Deep Learning)

14. PyTorch로 다층 퍼셉트론(MLP)을 설계하고 ReLU와 Softmax 활성화 함수 연결하기
15. 순방향(Forward) 연산과 오차 역전파(Backpropagation)의 수식을 수치 미분 코드와 비교 검증하기
16. 동일한 MLP 모델에 SGD, Momentum, Adam 옵티마이저를 각각 적용하여 수렴 속도 비교하기
17. PyTorch Dataset과 DataLoader를 구현하여 미니배치(Mini-batch) 단위로 데이터 학습시키기
18. 신경망 레이어 사이에 Dropout과 Batch Normalization을 추가하여 train/val loss 격차 줄이기

## 📋 4단계: 비정형 데이터 및 도메인 심화 (CV & NLP)

19. Convolution 레이어의 커널(Kernel), 스트라이드(Stride), 패딩(Padding)에 따른 출력 크기 계산하기
20. ResNet 사전 학습 모델을 가져와 이미지 분류(Image Classification) 파인튜닝 태스크 수행하기
21. LSTM/GRU 레이어를 활용하여 시계열 주가 예측 또는 텍스트 긍부정 분류 모델 만들기
22. Seq2Seq 모델의 디코더가 인코더의 특정 시점을 주목하도록 만드는 Dot-product Attention 구현하기
23. Transformer 아키텍처 논문을 읽고 멀티 헤드 어텐션(Multi-Head Attention) 블록 코드로 짜보기
24. Hugging Face Transformers 라이브러리로 BERT 또는 GPT 계열 모델 로드 후 커스텀 데이터로 파인튜닝하기

## 📋 5단계: MLOps 및 모델 양산화 (Production)

25. DVC로 대용량 데이터셋의 버전을 관리하고, MLflow를 연동하여 실험별 하이퍼파라미터와 가중치(Artifact) 로깅하기
26. 학습이 완료된 모델 가중치를 추출하여 FastAPI 기반의 실시간 추론(Inference) API 엔드포인트 만들기
27. PyTorch 모델을 ONNX 포맷으로 변환하고, TensorRT 또는 양자화(Quantization)를 적용해 추론 속도(Latency) 개선하기
28. Apache Airflow를 활용하여 매일 밤 새로운 데이터를 수집-전처리-모델 재학습-검증하는 워크플로우 파이프라인 자동화하기
29. ML 추론 애플리케이션을 Docker 이미지로 빌드하고 AWS SageMaker 또는 로컬 쿠버네티스(Kubernetes)에 배포하기
30. Evidently AI 또는 대시보드 툴을 활용하여 운영 서버에 들어오는 입력 데이터의 데이터 드리프트(Data Drift) 모니터링 체계 구축하기

# AI 엔지니어 로드맵

## 1단계: 개발 기초 및 프로그래밍

1. ~~파이썬 데이터 타입 (List, Dict, Set, Tuple) 복잡도 이해 및 활용~~
2. 객체지향 프로그래밍 (Class, 인스턴스, 상속) 구현해 보기
3. Decorator 및 Generator 개념 이해하고 코드에 적용하기
4. asyncio 라이브러리를 활용한 비동기(Asynchronous) 함수 작성하기
5. ~~Requests 및 HTTP 메서드(GET, POST, PUT, DELETE) 기초 다지기~~
6. ~~FastAPI 또는 Flask를 활용하여 간단한 REST API 서버 구축하기~~
7. ~~Git 필수 명령어 (commit, push, pull, branch, merge) 숙달하기~~
8. ~~GitHub 레포지토리 관리 및 PR(Pull Request) 워크플로우 경험하기~~
9. Dockerfile을 작성하고 나만의 파이썬 백엔드 앱 이미지 빌드하기
10. ~~리눅스 CLI 환경 명령어 (ls, cd, mkdir, grep, chmod, curl) 익히기~~
11. 넘파이(NumPy)를 활용한 행렬(Matrix) 표현 및 내적(Dot Product) 연산하기
12. 경사하강법(Gradient Descent)의 개념과 작동 원리 시각적으로 이해하기

## 2단계: LLM 및 프롬프트 엔지니어링

1. ~~OpenAI 및 Anthropic 개발자 계정 생성 및 API Key 발급받기~~
2. 파이썬 공식 SDK를 활용하여 ChatGPT/Claude 모델에 프롬프트 찌르기
3. ~~Hugging Face에서 무료 오픈소스 모델(Llama 등) 로컬에 로드해 보기~~
4. OpenAI Playground를 활용하여 System prompt, User prompt 분리 제어하기
5. Few-shot Prompting 패턴을 설계하여 원하는 출력 예시 주입하기
6. Chain-of-Thought (CoT)를 적용해 복잡한 추론 문제 해결하기
7. Pydantic 라이브러리를 결합해 AI 응답을 완전한 JSON 구조로 강제하기
8. 문맥 제한(Context Window) 개념과 토큰(Token) 계산법 익히기

## 3단계: 검색 증강 생성, RAG

1. PDF, TXT, Notion 등 외부 문서를 텍스트 데이터로 파싱(Parsing)하기
2. 문서 길이에 맞춰 적절하게 쪼개는 청킹(Chunking - Character, Semantic 등) 기법 적용하기
3. OpenAI의 Embedding API를 사용하여 텍스트를 고차원 벡터로 변환하기
4. ChromaDB(로컬) 또는 Pinecone(클라우드) 인스턴스 생성하기
5. ~~변환한 벡터 데이터를 Vector DB에 인덱싱(저장)하기~~
6. ~~사용자의 질문과 가장 유사도가 높은 문서 Top-K개 찾아내기 (Cosine Similarity)~~
7. ~~LangChain 또는 LlamaIndex를 활용하여 '문서 파싱-임베딩-조회-LLM 답변' 전 과정 자동화하기~~

## 4단계: AI 에이전트 및 오케스트레이션

1. OpenAI Function Calling (Tool Use) 스펙 문서 이해하기
2. LLM이 스스로 날씨 API나 계산기 함수를 골라 실행하게 만들기
3. ReAct (Reasoning and Acting) 프레임워크 패턴의 로그 분석하기
4. LangGraph 또는 CrewAI 프레임워크 공식 문서 튜토리얼 마스터하기
5. 에이전트가 상태(State)를 기억하며 루프를 도는 메모리 기능 구현하기
6. 역할을 분담한 멀티 에이전트(예: 기획 에이전트 + 코딩 에이전트) 협업 시스템 개발하기

## 5단계: 모니터링 및 배포, LLMOps

1. LangSmith 또는 Langfuse 계정을 생성하고 내 파이썬 프로젝트에 SDK 연동하기
2. LLM 호출의 단계별 지연 시간(Latency)과 비용(Token Cost) 대시보드로 추적하기
3. 유저의 악성 프롬프트(Prompt Injection)를 방지하는 Guardrail 필터링 구축하기
4. 완성된 AI 에이전트 파이프라인을 FastAPI 엔드포인트로 래핑하기
5. 서비스 전체를 docker-compose를 이용해 멀티 컨테이너 환경으로 묶기
6. AWS (EC2/ECS) 또는 Supabase/Vercel 등 클라우드 플랫폼에 완전한 백엔드 배포하기
