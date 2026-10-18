---
title: EP014 테트리스 게임 머신러닝 4개 + 딥러닝 1개로 최적화
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


## 작업 내용
- 2026.10.18 Windows에서 SDL2 gui로 테트리스 게임 머신러닝 4개 + 딥러닝 1개로 최적화

## 스크린샷
<img width="1547" height="752" alt="Image" src="https://github.com/user-attachments/assets/30634c0d-2e90-4ce0-af16-1331780539ea" />

## 로그
```
Cell 2: [평탄화 튜닝 완료] 지형 안정성 중심의 50000개 물리 데이터셋 빌드 성공.

[학습 Engine] 9차원 가치 추적형 5대 알고리즘 고도화 학습 시작...
1/5: LinearSVR 가치 모델 학습 중...
2/5: Random Forest Regressor 학습 중...
3/5: XGBoost Regressor(대결 리더) 학습 중...
4/5: Gradient Boosting Regressor 학습 중...
5/5: [대책 반영] 초고밀도 포화 방지형 Deep Learning 신경망 최적화 학습 중...

Cell 2: [평탄화 튜닝 완료] 지형 안정성 중심의 50000개 물리 데이터셋 빌드 성공.

Cell 3-1: 회귀 계열 .predict() 연산 교정 및 문법 버그 전면 보정 성공.
pygame 2.6.1 (SDL 2.28.4, Python 3.7.4)
Hello from the pygame community. https://www.pygame.org/contribute.html

[시스템] 매치 종료 감지: 5대 모델별 개별 의사결정 추적 로그 저장 중...
tetris_play_SVM.log 의사결정 지표 백업 완료.
tetris_play_Random_Forest.log 의사결정 지표 백업 완료.
tetris_play_XGBoost.log 의사결정 지표 백업 완료.
tetris_play_LightGBM.log 의사결정 지표 백업 완료.
tetris_play_Deep_Learning.log 의사결정 지표 백업 완료.
[시스템] 모든 알고리즘 상태 기록 완료.
```

## 개선 순서
1. 합성 데이터를 공통으로 생성하고, 피처 엔지니어링으로 개선
2. 초기 1줄 clear 조차 안되어서 로그를 출력하고 세부적으로 상태를 기록하도록 함. (1판 단위로)
3. 로그를 반복적으로 추적하면서, Classification model을 변경해야 함을 확인하고 전체적으로 수정
4. SVR은 학습시간이 오래 걸려서, LinearSVR로 변경
5. 머신러닝끼리 경쟁시켜봄
6. 마지막으로 딥러닝 추가해서 경쟁시켜봄
7. 딥러닝이 성능이 떨어짐. 개선방안 적용
8. 딥러닝이 최고점을 받도록 개선



