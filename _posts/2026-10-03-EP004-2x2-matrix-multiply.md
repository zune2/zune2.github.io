---
title: EP004 pytorch로 2x2 행렬곱 계산
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

```
1 2   X   5 6   =  19 22
3 4       7 8      43 50
```

## 2x2 행렬 A,B의 곱 - pytorch
``` python
import torch

# A: 2행 2열 (2, 2)
A = torch.tensor([[1, 2],
                  [3, 4]], dtype=torch.int32)


B = torch.tensor([[5, 6],
                  [7, 8]], dtype=torch.int32)

# 행렬곱 수행
result = torch.matmul(A, B)

print(result)

# 출력
# tensor([[19, 22],
#        [43, 50]], dtype=torch.int32)
# torch.Size([2, 2])
```
