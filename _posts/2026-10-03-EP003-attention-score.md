---
title: EP003 Attention Score
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

## Attention Score

- 한 단어가 문장 내의 다른 단어들과 얼마나 깊은 연관성(유사도)을 가지고 있는지 수치로 나타낸 점수
- 문장의 다른 단어들에 얼마큼 집중(Attention)해야 할까?

``` python
# Query: 질문 단어 "cat" [1.0, 2.0]
# Keys: 비교 대상 단어들 ["cat", "sat", "mat"]의 행렬
attention_scores = torch.matmul(query, keys.T)

print(attention_scores)
# 출력 결과: tensor([5.0000, 3.5000, 2.5000])
```

`tensor([5.0, 3.5, 2.5])`가 어텐션 스코어

* 5.0 : cat과 cat의 연관성 점수 $\rightarrow (1.0 \times 1.0) + (2.0 \times 2.0) = 5.0$
* 3.5 : cat과 sat의 연관성 점수 $\rightarrow (1.0 \times 0.5) + (2.0 \times 1.5) = 3.5$
* 2.5 : cat과 mat의 연관성 점수 $\rightarrow (1.0 \times 1.5) + (2.0 \times 0.5) = 2.5$


## 2. 점수가 주는 의미

   1. cat 자신에 집중 (5.0): 당연히 자기 자신과의 연관성이 가장 높게 나옴.
   2. sat에 집중 (3.5): 고양이(cat)가 지금 무엇을 하고 있는지 알려주는 중요한 행동 단어이므로 점수가 높게 책정
   3. mat에 집중 (2.5): 고양이가 앉아있는 장소적 배경이 되므로 어느 정도 연관성이 부여


## 3. 실제 모델에서는 Softmax

이 스코어에 Softmax(소프트맥스)라는 함수를 통과시켜 "합이 100%(1.0)가 되는 확률 값"으로 만들어서 사용.

* [5.0, 3.5, 2.5] $\rightarrow$ Softmax $\rightarrow$ [0.78, 0.17, 0.05] (예시)

이렇게 변환되면 의미가 훨씬 명확해 짐.

"고양이(cat)를 이해하기 위해 내 에너지의 78%는 자기 자신에, 17%는 앉다(sat)에, 5%는 매트(mat)에 집중"
