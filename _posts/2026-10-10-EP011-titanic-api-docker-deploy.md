---
title: EP011 titanic 모델을 Fast API 만들고 Docker로 배포
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

## Titanic Survival Prediction Model Serving Architecture

- 프로덕션 환경에 최적화된 머신러닝 서빙 파이프라인 구축 토이 프로젝트입 
- 모델링
- 데이터 유효성 검증
- 스케일링 전처리 이식
- FastAPI 웹 API 설계
- Docker 컨테이너화

> issue 2번에서 코드 확인하기

---

### 전체 서빙 아키텍처 (System Architecture)

본 프로젝트는 다음과 같은 데이터 흐름과 격리된 인프라 환경을 따릅니다:

```text
[Client Request] (test.sh / curl / Swagger UI)
       │
       ▼ (HTTP POST /predict with JSON Payload)
┌────────────────────────────────────────────────────────┐
│ Docker Container (python:3.10-slim 환경)                │
│                                                        │
│  FastAPI Web Server                                    │
│   ├── 1. Pydantic Data Validation (필수 피처/타입 검증)    │
│   │                                                    │
│   ├── 2. StandardScaler Transformation (sc)            │
│   │      (Kaggle 학습 시 고정된 Mean/Scale 적용)           │
│   │                                                    │
│   └── 3. Soft Voting Ensemble Model (ensemble_lr)      │
│          (3개 다른 규제의 Logistic Regression 결합)        │
└────────────────────────────────────────────────────────┘
       │
       ▼ (HTTP 200 OK with Predicted Probability)
[Client Response] (JSON: prediction_label, probability)
```

---

### ✨ 핵심 기술 스펙 및 구현 사항 (Key Implementations)

#### 1. Robust Machine Learning Modeling (Kaggle)
* **소프트 보팅 앙상블 (Soft Voting Ensemble):** 서로 다른 규제 성격(`L1 Lasso`, 강한 `L2 Ridge`, 완화된 `L2 Ridge`)을 가진 3가지 로지스틱 회귀 모델을 결합하여 개별 모델의 과적합(Overfitting)을 제어하고 예측의 일반화 성능을 극대화했습니다.
* **직렬화 (Asset Serialization):** 학습이 완료된 앙상블 모델(`ensemble_lr`)과 전처리에 사용된 표준화 객체(`StandardScaler`)를 각각 독립적인 바이너리 파일(`.pkl`)로 추출하여 완벽한 추론 재현성을 확보했습니다.

#### 2. Production-Grade API Design (FastAPI)
* **비동기 런타임 및 경량화:** 높은 동시성 처리를 위해 `FastAPI` 기반의 고성능 서빙 레이어를 구축했습니다.
* **엄격한 데이터 유효성 검증:** `Pydantic`을 활용해 인입되는 데이터의 스키마 및 범위를 검증함으로써 데이터 오염(Data Corruption)으로 인한 추론 에러를 사전에 차단했습니다.
* **결합 오차 원천 차단:** 캐글 학습 당시의 고유 피처 배열 순서(`['PassengerId', 'Pclass', 'Age', ... 'Embarked_2']`)를 스키마에 고정하여 데이터 정렬 불일치 문제를 완벽하게 해결했습니다.

#### 3. Containerized Infrastructure (Docker)
* **환경 격리 및 재현성:** `python:3.10-slim` 베이스 이미지를 기반으로 불필요한 레이어를 최소화한 경량 뼈대를 구축하고, 어느 인프라 환경에서나 즉시 구동할 수 있도록 애플리케이션을 가상화했습니다.

---

### 📂 폴더 구조 (Project Structure)

```text
titanic-api/
├── venv/                   # 파이썬 독립 가상환경
├── titanic_ensemble_lr.pkl # [Asset] 학습 완료된 앙상블 모델 객체
├── titanic_scaler.pkl      # [Asset] 학습 데이터 기준의 StandardScaler 객체
├── main.py                 # FastAPI 엔진 및 엔드포인트 핵심 소스코드
├── test.sh                 # Bash 기반 실전 CLI 테스트 스크립트
├── requirements.txt        # 컨테이너 종속성 명세서
└── Dockerfile              # 도커 이미지 빌드 시나리오 스크립트
```

---

### 가이드

#### 1. Docker를 이용한 배포 (권장 방식)

별도의 파이썬 환경 세팅 없이 명령어 단 두 줄로 서버를 구동합니다.

```bash
# 이미지 빌드
docker build -t titanic-server .

# 컨테이너 실행 (8000번 포트 포워딩)
docker run -d -p 8000:8000 --name titanic-app titanic-server
```

#### 2. 로컬 개발 환경 (Uvicorn)

```bash
# 가상환경 활성화 및 패키지 설치
source venv/bin/activate
pip install -r requirements.txt

# 개발 서버 가동 (핫 리로드 적용)
uvicorn main:app --reload
```

---

### API 테스트 및 결과 예시 (Verification)

#### CLI 테스트 (`test.sh`)

```bash
./test.sh

cat test.sh
#!/bin/bash
curl -X POST 'http://127.0.0.1:8000/predict' \
  -H 'Content-Type: application/json' \
  -d '{
  "PassengerId": 892,
  "Pclass": 1,
  "Age": 22.0,
  "SibSp": 0,
  "Parch": 0,
  "Fare": 80.0,
  "Sex_0": 1,
  "Sex_1": 0,
  "Embarked_0": 1,
  "Embarked_1": 0,
  "Embarked_2": 0
}'
```

**Output:**
```json
{
  "prediction_code": 1,
  "prediction_label": "Survived",
  "survival_probability": 0.9084
}
```
* **결과 해석:** 입력값(1등석, 22세 여성 승객 등)을 바탕으로 도커 내부 컨테이너의 앙상블 모델이 계산해 낸 결과이며, 해당 승객의 **생존 확률은 90.84%**로 예측되었습니다.


