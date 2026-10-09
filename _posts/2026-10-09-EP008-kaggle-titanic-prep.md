---
title: EP008 Kaggle - Titanic 풀이 SVM
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
tags:
  - Kaggle
categories:
toc: true
toc_sticky: true
toc_label: 목차
description: desc가 여기에
---




## 1. 데이터 전처리 및 피처 엔지니어링 요약

* 피처 엔지니어링 (정보 추출)

* 결측치(NaN) 처리
Age(나이)의 빈칸을 단순 전체 평균이 아닌, 앞서 만든 호칭(Title)별 나이 중앙값으로 세밀하게 그룹화

* 원-핫 인코딩 (수치화)
문자열 컬럼인 Sex, Embarked, Title을 pd.get_dummies()를 활용해 0과 1의 이진 피처로 쪼개어 수치형 행렬로 변환

* 정답지 분리 (Survived Drop)
학습 데이터에서 정답 컬럼인 Survived를 완전히 분리(drop)하여 모델이 정답을 미리 훔쳐보는 치팅(Data Leakage) 차단

* 피처 스케일링 (정규화)
거리 기반 알고리즘인 SVM 특성에 맞춰, 인코딩이 완료된 최종 피처들을 StandardScaler를 통해 평균 0, 분산 1의 표준화 데이터(X_train_scaled)로 변환


## 2. 과적합 방지 및 최종 SVM 모델링 코드 요약
- StandardScaler적용하고, SVM으로 풀이
- 피처 엔지니어링도 간단하게 해야 오히려 답이 올라감




## 공부해야 할 내용

### 1. 서포트 벡터 머신 (SVM) 이론

* 핵심 3요소: 초평면(Hyperplane), 마진 최대화(Margin), 서포트 벡터(Support Vectors)의 개념.
* 오분류 허용 조절: 하드 마진과 소프트 마진(C 파라미터)의 차이 및 규제 원리.
* 비선형 데이터 해결: 고차원 변환을 돕는 커널 트릭(Kernel Trick)과 RBF 커널, 그리고 곡률을 결정하는 감마(γ) 파라미터.

### 2. 데이터 전처리 및 피처 엔지니어링

* 인코딩의 차이: 원-핫 인코딩(One-Hot Encoding)과 라벨 인코딩(Mapping)의 개념 및 선형 모델에 미치는 수학적 영향.
* 피처 스케일링: 거리 기반 알고리즘(SVM)에서 표준화(StandardScaler)가 필수적인 이유.
* 파생 변수 생성: 도메인 지식을 활용한 비선형 관계 추출 (Title, FamilySize 생성의 효과).
* 데이터 누수(Data Leakage): 학습 전 정답지(Survived)를 안전하게 분리해야 하는 이유.

### 3. 머신러닝 평가 지표 및 모델 오차

* 혼동 행렬 (Confusion Matrix): 정탐, 오탐, 미탐 등 모델이 틀린 방향을 읽는 법.
* 트레이드 오프(Trade-off): 정밀도(Precision)와 재현율(Recall)의 반비례 관계 및 데이터 불균형을 극복하는 F1-Score.
* 로그 손실 (Log Loss): 단순 0과 1 맞춤 여부가 아닌, 모델이 예측한 '확률값의 정밀함(불확실성)'을 벌점으로 계산하는 원리.

### 4. 고급 모델링 및 과적합 제어

* XGBoost: 트리 기반 앙상블 알고리즘의 특징과 과적합을 막기 위한 규제 파라미터(max_depth, subsample).
* 앙상블 학습: 하드 보팅과 소프트 보팅(Soft Voting)의 차이, 순수 선형 모델 조합이 무의미한 수학적 이유.
* 과적합(Overfitting)과 일반화: 훈련 데이터 검증 점수(예: 정확도 97~100%)와 실제 캐글 리더보드 점수가 반대로 움직이는 현상(통계적 변동성)의 원인.


