---
title: AI 엔지니어 로드맵
layout: single
permalink: /books/
author_profile: true
comments: false
read_time: true
---

AI 엔지니어 로드맵 (총 30개 항목)

## 1단계: 개발 기초 및 프로그래밍

1. ~~파이썬 데이터 타입 (List, Dict, Set, Tuple) 복잡도 이해 및 활용~~
2. 객체지향 프로그래밍 (Class, 인스턴스, 상속) 구현해 보기
3. Decorator 및 Generator 개념 이해하고 코드에 적용하기
4. asyncio 라이브러리를 활용한 비동기(Asynchronous) 함수 작성하기
5. ~~Requests 및 HTTP 메서드(GET, POST, PUT, DELETE) 기초 다지기~~
6. ~~FastAPI 또는 Flask를 활용하여 간단한 REST API 서버 구축하기~~
7. ~~Git 필수 명령어 (commit, push, pull, branch, merge) 숙달하기~~
8. ~~GitHub 레포지토리 관리 및 PR(Pull Request) 워크플로우 경험하기~~
9. Dockerfile을 작성하고 나만의 파이썬 백엔드 앱 이미지 빌드하기
10. ~~리눅스 CLI 환경 명령어 (ls, cd, mkdir, grep, chmod, curl) 익히기~~
11. 넘파이(NumPy)를 활용한 행렬(Matrix) 표현 및 내적(Dot Product) 연산하기
12. 경사하강법(Gradient Descent)의 개념과 작동 원리 시각적으로 이해하기

## 2단계: LLM 및 프롬프트 엔지니어링

1. ~~OpenAI 및 Anthropic 개발자 계정 생성 및 API Key 발급받기~~
2. 파이썬 공식 SDK를 활용하여 ChatGPT/Claude 모델에 프롬프트 찌르기
3. Hugging Face에서 무료 오픈소스 모델(Llama 등) 로컬에 로드해 보기
4. OpenAI Playground를 활용하여 System prompt, User prompt 분리 제어하기
5. Few-shot Prompting 패턴을 설계하여 원하는 출력 예시 주입하기
6. Chain-of-Thought (CoT)를 적용해 복잡한 추론 문제 해결하기
7. Pydantic 라이브러리를 결합해 AI 응답을 완전한 JSON 구조로 강제하기
8. 문맥 제한(Context Window) 개념과 토큰(Token) 계산법 익히기

## 3단계: 검색 증강 생성, RAG

1. PDF, TXT, Notion 등 외부 문서를 텍스트 데이터로 파싱(Parsing)하기
2. 문서 길이에 맞춰 적절하게 쪼개는 청킹(Chunking - Character, Semantic 등) 기법 적용하기
3. OpenAI의 Embedding API를 사용하여 텍스트를 고차원 벡터로 변환하기
4. ChromaDB(로컬) 또는 Pinecone(클라우드) 인스턴스 생성하기
5. ~~변환한 벡터 데이터를 Vector DB에 인덱싱(저장)하기~~
6. ~~사용자의 질문과 가장 유사도가 높은 문서 Top-K개 찾아내기 (Cosine Similarity)~~
7. ~~LangChain 또는 LlamaIndex를 활용하여 '문서 파싱-임베딩-조회-LLM 답변' 전 과정 자동화하기~~

## 4단계: AI 에이전트 및 오케스트레이션

1. OpenAI Function Calling (Tool Use) 스펙 문서 이해하기
2. LLM이 스스로 날씨 API나 계산기 함수를 골라 실행하게 만들기
3. ReAct (Reasoning and Acting) 프레임워크 패턴의 로그 분석하기
4. LangGraph 또는 CrewAI 프레임워크 공식 문서 튜토리얼 마스터하기
5. 에이전트가 상태(State)를 기억하며 루프를 도는 메모리 기능 구현하기
6. 역할을 분담한 멀티 에이전트(예: 기획 에이전트 + 코딩 에이전트) 협업 시스템 개발하기

## 5단계: 모니터링 및 배포, LLMOps

1. LangSmith 또는 Langfuse 계정을 생성하고 내 파이썬 프로젝트에 SDK 연동하기
2. LLM 호출의 단계별 지연 시간(Latency)과 비용(Token Cost) 대시보드로 추적하기
3. 유저의 악성 프롬프트(Prompt Injection)를 방지하는 Guardrail 필터링 구축하기
4. 완성된 AI 에이전트 파이프라인을 FastAPI 엔드포인트로 래핑하기
5. 서비스 전체를 docker-compose를 이용해 멀티 컨테이너 환경으로 묶기
6. AWS (EC2/ECS) 또는 Supabase/Vercel 등 클라우드 플랫폼에 완전한 백엔드 배포하기
