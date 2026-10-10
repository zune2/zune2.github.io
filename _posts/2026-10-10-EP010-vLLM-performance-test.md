---
title: EP009 vLLM이란?
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

## vLLM
https://youtu.be/OfpGLIUuzww?si=s2Ab77xca2mwcO0S

- PagedAttention
- 병렬처리 능력 커짐
- 단일 작업 처리에서는 큰 차이가 없으나, 다수의 병렬처리에서 큰 성능 차이를 보임.
- Ollama와 성능 비교 나옴

## 시사점
- 운영체제에서 배웠던 페이징 기법을 LLM의 최적화에 사용함.
