## Classification
- 많은 인공지능 문제들 -> 분류 문제로 변환
	- 자동차 운전
	- 문장, 단어의 의미 분류
- **복잡한 문제를 명확, 구조화된 선택으로 단순화** -> 문제 해결의 효율성 ↑

## 분류란?
- **==입력 데이터가 주어졌을 떄, 이를 특정 클래스에 할당하는 과정==**
	- 다양한 형태의 입력(숫자, 기호), 출력(클래스 레이블) 처리
- 기본 접근 방법들
	- **확률 모델 기반** : 입력 데이터가 특성 클래스에 속할 활률 계산
		- 베이지안 분류기
	- **뉴럴 네트워크 기반** : 딥러닝 기술 활용 -> 복잡한 패턴, 데이터 구조 학습
	- **통계 및 규칙 기반** : 데이터의 통계적 속성이나 사전 정의 규칙 사용
		- 불확실성 모델링 강점
- 각 분류기 종류? 핵심 아이디어는? 

## 분류 문제의 다양한 접근 방식

![[classification_methods.webp]]

### 선 기반 분류 (Line-based Classification)
- **데이터 분리하는 결정 경계를 선형으로 설정**
- 간단, 계산 효율 ↑

- **로지스틱 회귀** : 결과를 확률로 표현하여 특정 클래스에 속할 확률 계산
- **서포트 벡터 머신** : 데이터 클래스 사이의 마진을 최대화하는 선을 찾아 최적의 분류 경계 설정

### 거리 기반 분류 (Distance-based Classification)
- **데이터 포인트 간의 거리를 측정하여 가장 가까운 데이터의 클래스로 분류**

- **K-최근접 이웃(K-Nearest Neighbors, KNN)** : 입력 데이터와 가장 가까운 K개의 훈련 데이터 찾고, 최빈 클래스를 결과로 선택

### 확률 기반 분류 (Probabilistic Classification)
- 입력 클래스가 각 클래스에 속할 확률을 기반으로 분류 수행

- **나이브 베이지안(Naive Bayes) 분류기** : 특성들의 독립성 가정, 베이즈 정리 사용해 각 클래스의 조건부 확률 계산

### 트리 기반 분류 (Tree-based Classification)
- 결정 트리 사용해 데이터를 여러 단계에 걸쳐 분류

- **결정 트리(Decision Tree)** : 데이터 특성을 기준으로 트리 구조 생성, 각 노드에서 질문 통해 데이터 분리

### 신경망 기반 분류 (Neural Network-based Classification)
- 복잡한 데이터 패턴을 추상화
- 다양한 형태 데이터에 대해 효과적인 분류 제공, 직접 분류 수행

- **인공신경망(ANN)** : 여러 층을 통해 데이터에서 고차원 특성 추출, 이를 저차원 벡터로 추상화( # of classes 만큼) -> a.k.a low-dimenstion projection based 방식

### 프롬프트 기반 분류 (Prompt-based Classification)
- 언어 모델 이용 분류에서 강력한 성능

- **언어 모델 기반 분류** : 주어진 프롬프트에 따라 언어 모델이 적절한 답변 생성, 이를 분류 기준으로 사용

<hr>

## 거리 기반 분류(Distance-based Classification)
- 데이터 사이의 거리 계산 -> 가장 가까운 데이터의 클래스를 할당
- 직관적, 구현 간단

### 작동 원리
1. **데이터 분할** : 알려진(훈련) 데이터를 각 클래스에 따라 구분하고 위치를 결정
2. **새로운 입력 처리** : 새로운 입력 데이터가 들어오면, 데이터 공간 내에서 위치 찾고, **입력 데이터와 알려진 각 데이터 포인트 간의 거리 계산**
3. **가장 가까운 데이터 찾기** : 계산된 거리 기반, 입력 데이터와 가장 가까운 데이터의 클래스를 배정

### 주요 특징
- **직관적인 접근** : 사람의 직관적인 판단 방식과 유사
- **간단한 구현** : 복잡한 확률 계산, 고도의 훈련 X
- **유연성과 확장성** : 거리 계산 방법을 다양하게 선택, 차원이 늘어나도 적용 가능

### 적용 예시
- 고객, 이미지 분류, 추천 시스템 등 다양한 분야 활용
- 단점
	- 복잡한 데이터엔 쫌 ;;
	- 데이터 포인트 증가할수록 속도 ↓
-  젤 인기 테크닉 -> **KNN 알고리즘**
	- 주어진 데이터 주변의 k개의 가장 가까운 이웃을 찾아 최빈 클래스
	- 불명확, 비정형 데이터에 강력한 성능
		- 구매이력 기반 사용자 패턴, 음성 데이터 분류


## 선 기반 (Line-Based Approach) 분류
- **가장 흔히 사용되는 강력하괴 직관적인 분류 기술**
- 공간 내에서 데이터를 두 개 이상의 그룹으로 나누는 경계선을 찾는 것이 목표

### 작동 원리
1. **데이터 프로젝션** : 모든 데이터 포인트를 특정 공간에 투영, 공간은 데이터 특성에 따라 정의
2. **결정 경계 설정** : 데이터 공간을 나누는 선을 결정
3. **카테고리 할당** : 선을 경계로 카테고리를 할당

### 주요 기술
- **로지스틱 회귀** : 데이터 포인트가 특정 카테고리에 속할 확률을 계산 -> 최적의 결정 경계 탐색
- **서포트 벡터 머신(SVM)** : 카테고리 간의 마진을 최대화하는 선을 찾음, 견고한 분류 경계 제공
	- 경계가 명확하게 구분되어야 할 때 유용

### 장점
- **명확성과 간결성** : 선 기반 분류를 계산이 간단, 결과 해석 용이
- **효율적인 성능** : 적절한 데이터셋, 매개변수 조정 통해 높은 정확도 가능

### 적용 분야
- 은행 신용 평가, 의료 진단, 이미지 처리, ...
- 선을 사용해 데이터 효과적 분리, 카테고리에 정확히 할당
- 간단함, 효율성
- 복잡한 데이터 구조에서도 확실한 경계 설정, 빠르고 정확한 분류 결과 제공


## 저차원 투사 기반 Classification (Low Dimensional Projection based Classification)
- **고차원 데이터를 저차원으로 투사**
	- 이미지, 텍스트 등 고차원 데이터에 좋음
- 고차원의 데이터를 -> **저차원(클래스의 수)으로 변환**

### 작동 원리
1. **고차원 데이터의 입력**
2. **저차원으로의 투사** : 신경망으로 입력 고차원 데이터 -> 저차원 데이터 투사
	- 신경망은 복잡한 데이터 구조에서 중요한 특성만을 추출
3. **클래스 결정** : 저차원 투사된 데이터는 미리 정의된 클래스의 차원 따라 분류
	- 분류군이 세 가지면, 최종 벡터는 3차원

### 주요 이점
- **계산 효율성 증대** : 데이터 차원 줄임으로써 계산량, 리소스 ↓, 대규모 데이터셋 유용
- **특성 강조** : 중요한 특성이 강조, 분류기의 성능이 향상
- 고품질 인코더 통해서 구현도 용이

### 적용 사례
- 데이터 복잡성 관리, 효율적인 분석
- 고급 알고리즘(신경망)과 결합하여 강력한 성능
- 이미지, 음성 인식, 텍스트 분석 등


## 프롬프트 기반 분류 (Prompt-based Classification )에 대한 이해
- 최근 언어모델의 성장과 함께 나타난 새로운 형태의 분류 테크닉
- 파라메트릭 방식 vs 비파라메트릭 방식
- 트랜스포머의 '헤드 기반' vs '프롬프트 기반'

### 파라메트릭 vs 비파라메트릭 분류 방식 비교
#### Parametric Classification
- 미리 정의된 모델 구조`(y = ax + b)` 가짐 ->  주어진 데이터에서 모델 파라미터`(a, b) `학습
	- 구조가 명확, 계산 효율 좋음, 데이터 요구량 적음
	- 복잡하거나 노이즈가 많은 데이터에는 유연성 ↓
- 분류용 전문 Parameters를 데이터로부터 학습

#### Nonparametric Classification
- 분류 모델을 사전에 정의 X -> 데이터에서 패턴을 찾아냄
- 많은 양의 데이터 필요, 관계 이해 유연해짐
	- 계산 비용, 메모리 요구 ↑
- 분류용 전문 Parameters가 없거나 학습 X

### 헤드 기반(Head-based) 분류
1. **정의 :**  이미 선학습 된 모델을을 가져와, 우리가 원하는 분류 수행 위해 추가 레이어 부착 -> 재학습
2. **특징 :** 명확하게 정의된 param 바탕으로 학습 진행
	- 트랜스포머 : 최상층 레이어에서 얻은 벡터값 이용, 클래스 수만큼 저차원 투사하는 Head Layer를 학습
3. **파라미터 필요성 :** 고차원 -> 저차원 줄이기 위해 파라미터 필요
4. **트레이닝 요구 :** 명확한 학습 단계 필요 -> 최적화된 결과 도출
- Transformer의 헤드기반 분류 방식은 **파라메트릭 방식**

### 프롬프트 기반 (Prompt-based) 분류
1. **정의** : 미리 정의된 클래스 없이, 입력된 데이터를 바탕으로 적접적인 해석, 연관성 찾아 결과를 도출
	- 고정된 파라미터 X
	- 입력에 대한 출력 동적 생성
2. **클래스 가정 부재 :** 분류할 클래스 사전 강의 X -> 매우 유연
3. **트레이닝 비요구 :** 명확한 학습 단계 X -> 입력 데이터와 연동하여 동적 반응

- **언어 모델이 출력한 어휘를 바탕으로 분류를 수행**
- Prompt를 입력해 나온 출력에 대한 후처리 -> non-parametric 방식
- 프롬프트 기반 분류 zero-shot transferable 기술 이용한 연구 : **CLIP**


## 결론
- 상황에 맞는 적절한 기술 선택
- 트랜스포머 기반 파라메트릭 기술이 높은 성능
- 허나, LLM 성능이 좋아지면서 prompt도 뜨고 있음