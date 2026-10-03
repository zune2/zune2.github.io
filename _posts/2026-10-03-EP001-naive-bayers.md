---
title: 나이브 베이즈로 스팸 필터링
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
tags:
popular: true
  - Git
categories:
toc: true
toc_sticky: true
toc_label: 목차
description: desc가 여기에
---


## 1. 베이즈 정리 기본 공식

특정 단어들이 주어졌을 때, 이 메일이 스팸(1)일 확률 $P(Spam\vert{}X)$를 구하는 공식

$$P(Spam\vert{}X) = \frac{P(X\vert{}Spam) \times P(Spam)}{P(X)}$$ 

* $P(Spam\vert{}X)$ (사후 확률): 어떤 이메일에 단어들($X$)이 들어있을 때, 이 메일이 스팸일 확률 (우리가 구하고자 하는 값)
* $P(X\vert{}Spam)$ (우도 / Likelihood): 실제 스팸 메일 중에서 해당 단어들($X$)이 등장할 확률
* $P(Spam)$ (사전 확률): 전체 메일 중 스팸 메일이 차지하는 비율
* $P(X)$: 전체 메일에서 해당 단어들($X$)이 등장할 확률


## 2. 왜 '나이브(Naive, 순진한)' 베이즈일까?

- 이메일에는 단어가 1개가 아니라 여러 개($x_1, x_2, x_3, ...$)가 있음.
- 예를 들어 '무료(x1)', '대출(x2)'이라는 단어가 동시에 들어있다면 원래는 두 단어의 연관성까지 고려해야 해서 계산이 복잡해짐.
- 나이브 베이즈는 "모든 단어들은 서로 완전히 독립적이다"라고 아주 순진하게(Naive) 가정
- 이 가정 덕분에 복잡한 결합 확률 공식이 단순한 곱셈이 됨
  
$$P(X\vert{}Spam) = P(x_1\vert{}Spam) \times P(x_2\vert{}Spam) \times P(x_3\vert{}Spam) \times ...$$ 


## 3. 실제 스팸 분류기 계산 공식

컴퓨터가 이메일을 받았을 때, 이 메일이 스팸(Spam)일 확률과 정상(Ham)일 확률을 각각 계산한 뒤 더 큰 쪽으로 분류

$$\text{Spam Score} = P(Spam) \times P(x_1\vert{}Spam) \times P(x_2\vert{}Spam) \times ...$$ 
$$\text{Ham Score} = P(Ham) \times P(x_1\vert{}Ham) \times P(x_2\vert{}Ham) \times ...$$ 

* 최종 결론: 만약 $\text{Spam Score} > \text{Ham Score}$ 이면 이 메일은 스팸으로 분류.

## 예시
전체 메일 10개 중 스팸이 5개, 정상이 5개 ($P(Spam) = 0.5$, $P(Ham) = 0.5$)

* 스팸 메일 5개 중 '무료'라는 단어는 4번 $\rightarrow P('무료'\vert{}Spam) = \frac{4}{5} = 0.8$
* 정상 메일 5개 중 '무료'라는 단어는 1번 $\rightarrow P('무료'\vert{}Ham) = \frac{1}{5} = 0.2$

이때 "무료"라는 단어가 포함된 새 이메일이 들어왔다면?

   1. 스팸일 확률 점수: $P(Spam) \times P('무료'\vert{}Spam) = 0.5 \times 0.8 = \mathbf{0.4}$
   2. 정상일 확률 점수: $P(Ham) \times P('무료'\vert{}Ham) = 0.5 \times 0.2 = \mathbf{0.1}$

결과: 스팸 점수($0.4$)가 정상 점수($0.1$)보다 크기 때문에 컴퓨터는 이 메일을 스팸 메일로 판단
