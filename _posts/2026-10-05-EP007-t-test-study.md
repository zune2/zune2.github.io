---
title: EP007 t-test란?
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
tags:
  - Pytorch
categories:
toc: true
toc_sticky: true
toc_label: 목차
description: desc가 여기에
---

## t-test란?
- 두 집단의 평균 차이가 통계적으로 유의미한지 확인하는 가설 검정 방법

### t-값

1. 두 집단 사이의 평균 차이를 데이터의 불확실성(표본오차)로 나눈 값.
2. 그룹 간의 평균 차이가 클수록, 데이터의 변동성(흩어진 정도)이 작고 표본수가 클수록 t값이 커짐
3. 통계적으로 유의미한 차이가 있다고 결론내리는 확률 (p-value < 0.05)

## t검정의 종류

### One-Sample t-test
단일표본 t-검정
- 우리나라 남성 평균키가 175 cm인가?

### Independent two-sample t-test
독립표본 t검정
- A반과 B반의 수학성적 평균에 차이가 있는가?
- 흡연자, 비흡연자의 혈압 차이
  
### Paired-sample t-test
대응표본 t검정
- 다이어트약 복용 전후의 몸무게 평균의 차이

## 가정 조건 (주의사항)
1. 정규성을 만족해야 한다.
  - 데이터가 치우치지 않고, 종 모양의 정규분포를 따른다.
2. 등분산성을 만족해야 한다.
  - 두 집단의 분산이 비슷함
   
