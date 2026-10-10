---
title: EP012 Tabular Playground 2021 May 풀기
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

- https://www.kaggle.com/competitions/tabular-playground-series-may-2021

- 보기 (객관식 선택지): [Class_1, Class_2, Class_3, Class_4] 4지선다형
- 데이터 피처: 이커머스 고객들의 행동 피처(비식별화된 수치 데이터 50여 개)
- 평가지표로 Multi-class Log Loss를 사용하기 때문에 모델이 찍은 정답의 확률 분포가 얼마나 정교한지 철저하게 검증 가능

- 데이터에 결측치는 존재하지 않음
- feature importance 구하고 시작
- 1.09696까지 나옴

lightGBM, Optuna 하이퍼파라미터 최적화 -> 이전보다 나아지지는 않았음.

