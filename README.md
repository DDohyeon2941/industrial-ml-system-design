# Industrial ML System Design

## Overview

실제 산업 데이터 환경에서 수행한 Machine Learning 시스템 설계 경험과
데이터 처리 구조를 정리한 저장소입니다.

산업 데이터 환경에서는 데이터 정합성 문제, 시계열 불일치,
대용량 데이터 처리, 운영 환경 제약 등 다양한 문제가 동시에 발생합니다.

본 저장소는 이러한 문제들을 실제 프로젝트에서 어떻게 해결하고자 했는지,
그리고 어떤 방향으로 ML 시스템을 설계했는지를 중심으로 정리합니다.

특정 고객사 및 내부 시스템 정보는 제외하였으며,
일반화 가능한 문제 구조와 해결 접근 방식을 중심으로 작성하였습니다.

---

# Industrial AI Projects

# 1. Battery Manufacturing ML System

## Overview

2차전지 전구체 제조 공정 데이터를 활용하여
Ni, Co, Mn, Li 등 주요 성분 값을 예측하는
머신러닝 시스템을 설계한 프로젝트입니다.

공정 센서 데이터와 분석 데이터의 수집 주기가 서로 달랐으며,
시계열 정합성 문제를 해결하기 위한
feature engineering 및 데이터 동기화 구조 설계가 핵심 과제였습니다.

---

## Key Challenges

### Irregular Sampling Interval

센서별 데이터 수집 간격이 서로 달라
동일 시점 기준으로 데이터를 직접 비교하기 어려웠습니다.

일부 데이터는 초 단위,
일부 분석 데이터는 수분~수시간 단위로 기록되어
시계열 기반 동기화 구조가 필요했습니다.

---

### Timestamp Mismatch

공정 데이터와 분석 데이터 간 timestamp mismatch가 존재하였으며,
실제 공정 시점과 데이터 저장 시점 간 차이도 발생했습니다.

이로 인해 target leakage를 방지하면서
의미 있는 feature를 생성하는 과정이 필요했습니다.

---

### Feature Consistency

동일 변수라도 공정 상황에 따라 분포가 달라졌으며,
공정 구간별 특성을 반영한 feature engineering이 필요했습니다.

특히 rolling statistics 및 변화량 기반 feature 생성이 중요했습니다.

---

## My Contributions

- 시계열 기반 데이터 동기화 로직 설계
- rolling / diff / aggregation 기반 feature engineering
- 공정 구간 기반 변수 생성
- multivariate manufacturing time-series 처리
- 성분별 개별 ML pipeline 구축
- 모델 학습 / 검증 / 예측 파이프라인 모듈화
- 모델별 성능 비교 구조 설계
- 데이터 정합성 검증 로직 설계

---

## Key Learnings

- 산업 데이터에서는 데이터 정합성이 모델 복잡도보다 중요할 수 있음
- Feature Engineering이 모델 성능에 큰 영향을 미침
- 실제 운영 환경에서는 inference 안정성과 유지보수성을 함께 고려해야 함

---

# 2. Manufacturing Inspection AI System

## Overview

제조 검사 데이터를 기반으로
품질 안정화를 위한 압력 추천 시스템 및
Industrial AI 데이터 파이프라인 구조를 설계한 프로젝트입니다.

검사 장비와 생산 시스템 간 데이터 구조 차이,
대규모 bump-level 데이터 처리,
공정 간 데이터 정합성 문제가 핵심 과제였습니다.

---

## Key Challenges

### Multi-source Inspection Data

여러 검사 장비 및 생산 시스템에서
서로 다른 구조의 데이터가 생성되었습니다.

파일 구조, timestamp 기준,
식별 체계 등이 서로 달라
데이터 통합 과정에서 정합성 검증이 필요했습니다.

---

### Large-scale Manufacturing Data

bump-level 데이터와 같이
고용량 제조 데이터를 처리해야 했으며,
효율적인 staging 구조와 적재 전략이 필요했습니다.

특히 parquet 기반의 데이터 처리 구조를 검토하며,
대규모 데이터 처리 효율 개선을 고려했습니다.

---

### Process Alignment

공정 간 strip / unit alignment 문제로 인해
동일 생산 단위를 연결하는 과정이 필요했습니다.

또한 생산 데이터와 검사 데이터 간
timestamp inconsistency 문제도 함께 존재했습니다.

---

### Production Constraints

실제 생산 환경에서는
단순 모델 성능보다 운영 가능성과 안정성이 중요했습니다.

데이터 수집 방식,
검사 흐름,
실시간 추론 가능성 등을 함께 고려해야 했습니다.

---

## My Contributions

- 제조 검사 데이터 ETL 구조 설계
- parquet 기반 staging 구조 검토
- inspection timestamp validation 로직 설계
- multi-source manufacturing data integration
- 데이터 품질 검증 기준 정의
- inspection data consistency 검증
- 압력 추천 시스템을 위한 데이터 구조 설계
- 운영 환경 기반 평가 기준 및 활용 전략 논의
- production ML pipeline 구조 검토

---

## Key Learnings

- 실제 산업 데이터는 이상적인 구조로 존재하지 않음
- 데이터 품질 검증이 ETL 과정에서 매우 중요함
- 운영 가능한 ML 구조 설계가 핵심
- 시스템 관점의 접근이 모델 자체보다 중요할 수 있음

---

# Technical Keywords

- Manufacturing AI
- Industrial Machine Learning
- Time-Series Analysis
- Feature Engineering
- ETL Pipeline
- Data Consistency Validation
- Multi-source Data Integration
- Production ML System
- Large-scale Data Processing
- Manufacturing Inspection Data
- Imbalanced Learning

---

# Disclaimer

본 저장소는 산업 데이터 환경에서의 경험 및 문제 해결 방향을 정리한 저장소이며,
특정 고객사 및 내부 시스템 정보는 포함하지 않습니다.

모든 내용은 일반화된 형태로 작성되었습니다.
