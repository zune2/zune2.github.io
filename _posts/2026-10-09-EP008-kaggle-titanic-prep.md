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
