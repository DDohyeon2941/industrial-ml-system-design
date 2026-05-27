# Industrial ML System Design

## Overview

실제 산업 데이터 환경에서는 데이터가 이상적인 형태로 존재하지 않습니다.
센서별 수집 주기의 차이, 생산 데이터 누락, 검사 데이터 정합성 문제,
운영 환경의 제약 등 다양한 문제가 동시에 발생합니다.

본 저장소는 실제 산업 데이터 환경에서 수행한 Machine Learning 시스템 설계 경험과
데이터 처리 과정에서의 문제 해결 방향을 정리한 저장소입니다.

특정 고객사 및 내부 시스템 정보는 제외하였으며,
산업 데이터 환경에서 공통적으로 발생하는 문제와
이를 해결하기 위한 접근 방식을 중심으로 작성하였습니다.

---

# Industrial AI Projects

## 1. Battery Manufacturing ML System

### Overview

2차전지 전구체 제조 데이터를 활용하여
주요 품질 지표를 예측하는 머신러닝 시스템을 설계한 프로젝트입니다.

센서 및 분석 데이터의 수집 주기가 서로 달랐으며,
시계열 정합성 문제를 해결하기 위한 feature engineering과
데이터 동기화 구조 설계가 핵심 과제였습니다.

---

### Key Challenges

#### 1) Irregular Time-Series

센서별 데이터 수집 간격이 서로 달라
동일 시점 기준으로 데이터를 직접 비교하기 어려웠습니다.

예를 들어,
일부 센서는 초 단위,
일부 분석 데이터는 수분~수시간 단위로 기록되어
시간축 정렬이 필수적이었습니다.

---

#### 2) Data Synchronization

생산 데이터와 분석 데이터 간 timestamp mismatch가 존재하였고,
실제 공정 흐름과 데이터 저장 시점 간 차이도 발생했습니다.

이로 인해 target leakage를 방지하면서
의미 있는 feature를 생성하는 과정이 필요했습니다.

---

#### 3) Production Data Quality

실제 생산 환경에서는
누락값, 이상치, 비정상 구간 등이 지속적으로 발생하였습니다.

또한 동일 변수라도
공정 상황에 따라 분포가 달라지는 문제가 존재했습니다.

---

### My Contributions

- 시계열 기반 데이터 정렬 로직 설계
- rolling statistics 기반 feature engineering
- 공정 구간 기반 변수 생성
- multivariate manufacturing time-series 처리
- 모델 학습/검증 파이프라인 구조화
- 모델별 성능 비교 및 재현 가능한 구조 설계

---

### Key Learnings

- 산업 데이터에서는 데이터 정합성이 모델 복잡도보다 중요할 수 있음
- Feature Engineering이 모델 성능에 미치는 영향이 매우 큼
- 실제 운영 환경에서는 inference 안정성을 함께 고려해야 함

---

# 2. Manufacturing Inspection AI System

### Overview

제조 검사 데이터를 기반으로
품질 예측 및 데이터 파이프라인 구조를 설계한 프로젝트입니다.

여러 생산 및 검사 시스템에서 생성된 데이터를 통합하고,
대규모 제조 데이터를 처리하기 위한 ETL 및 staging 구조를 검토하였습니다.

---

### Key Challenges

#### 1) Multi-source Inspection Data

여러 검사 장비 및 생산 시스템에서
서로 다른 구조의 데이터가 생성되었습니다.

파일 구조, timestamp 기준, 식별 체계 등이 달라
데이터 통합 과정에서 정합성 검증이 필요했습니다.

---

#### 2) Large-scale Manufacturing Data

대규모 제조 데이터를 처리해야 했으며,
효율적인 staging 구조와 적재 전략이 필요했습니다.

특히 bump-level 데이터와 같이
고용량 데이터 처리 시 저장 구조 최적화가 중요했습니다.

---

#### 3) Data Consistency Validation

실제 운영 환경에서는
검사 데이터 누락, timestamp 오류,
식별 정보 불일치 등의 문제가 반복적으로 발생했습니다.

따라서 단순 적재가 아닌,
검증 가능한 ETL 구조 설계가 필요했습니다.

---

#### 4) Production ML Constraints

실제 생산 환경에서는
모델 성능뿐 아니라 운영 가능성과 안정성이 중요했습니다.

데이터 수집 방식,
운영 프로세스,
실시간 추론 가능성 등을 함께 고려해야 했습니다.

---

### My Contributions

- 제조 검사 데이터 ETL 구조 설계
- parquet 기반 staging 구조 검토
- inspection timestamp validation 로직 설계
- multi-source manufacturing data integration
- 데이터 품질 검증 기준 정의
- 운영 환경을 고려한 ML pipeline 구조 검토
- 평가 기준 및 데이터 활용 전략 논의

---

### Key Learnings

- 실제 산업 데이터는 이상적인 구조로 존재하지 않음
- 데이터 품질 검증이 ETL에서 매우 중요함
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
- Imbalanced Learning

---

# Disclaimer

본 저장소는 산업 데이터 환경에서의 경험 및 문제 해결 방향을 정리한 저장소이며,
특정 고객사 및 내부 시스템 정보는 포함하지 않습니다.
모든 내용은 일반화된 형태로 작성되었습니다.
