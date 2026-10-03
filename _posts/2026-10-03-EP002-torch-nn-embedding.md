---
title: EP002 nn.Embedding의 동작
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

### nn.Embedding의 역할

- nn.Embedding은 단어의 정수 인덱스(Index)를 고정된 크기의 연속적인 벡터(Vector)로 매핑해 주는 PyTorch의 룩업 테이블(Lookup Table)
- 가로 길이가 embedding_dim이고, 세로 길이가 num_embeddings인 하나의 행렬(Weight Matrix)을 내부에 들고 있는 것
- 내부에 선언된 행렬은 고정된 상수가 아님.
- PyTorch의 nn.Parameter로 지정되어 있어, 모델이 손실 함수(Loss)를 줄여가는 과정에서 오차역전파(Backpropagation)를 통해 단어 벡터의 숫자 값들이 자동으로 업데이트


``` python
# 표준정규분포 규칙으로 채워진 임베딩 행렬 예시
[
  [ 0.12, -0.05,  0.89,  0.23 ],  # 대부분 0 근처의 작은 숫자들
  [-0.77,  0.11, -0.34,  1.56 ],  # 가끔 1을 조금 넘는 숫자도 나옴 (1.56)
  [ 0.05,  0.42, -0.12, -0.08 ]   # 역시나 0 근처가 밀집됨
]
```
- 아무런 설정을 하지 않으면, PyTorch는 내부적으로 평균이 0이고 표준편차가 1인 표준정규분포를 사용하여 무작위로 행렬을 채움.
- torch.randn과 완벽히 동일한 원리로 동작


### nn.Embedding(3, 4)를 선언하면

- 컴퓨터 메모리에는 3행 4열짜리 가중치 행렬(Weight Matrix)이 생성
- 컴퓨터는 단어 사전의 인덱스 번호를 이 행렬의 행 번호(Row)로 정확하게 매핑.

```
단어 사전 (Vocabulary)           내부 가중치 행렬 (Weight Matrix)
"cat" -> 인덱스 0  ----------->  [Row 0]  [ 0.12, -0.45,  0.89,  0.23 ]
"sat" -> 인덱스 1  ----------->  [Row 1]  [-0.77,  0.11, -0.34,  0.56 ]
"mat" -> 인덱스 2  ----------->  [Row 2]  [ 0.65,  0.92, -0.12, -0.88 ]
```

• `embedding(torch.tensor([0]))`을 호출하면 내부 행렬의 0번째 행을 통째로 떼어다가 반환.
• 이처럼 곱셈이나 덧셈 연산 없이, 메모리에 저장된 특정 주소의 행을 그대로 가져오기 때문에 이를 룩업 테이블(Lookup Table)이라고 부름.

