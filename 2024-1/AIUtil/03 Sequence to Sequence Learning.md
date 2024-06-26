## 개요
- `Seq2Seq`은 `RNN`이나 `Transformer` 같은 특정 아키텍쳐나 기술적 방법론이 아님
	- 문제 해결에 적용하는 ==**틀**==이나 **==프레임워크==**
- 음성인식이나 영상처리 등 문제에 **기존 구현체들 활용** -> 상대적으로 안정된 성능

## Sequence to Sequence를 통한 ML의 외연확장
- 전통적 문제, 기존 방식 : 사람의 인지 기관을 모방
	- 얼굴 인식, 음성 인식, 물체 인식, 자연어 처리
- Seq2Seq로 범위 확장
	- 비전문가도 데이터만 충분하면, 성능이 보장된 Seq2Seq 모델로 문제 해결 가능

## Sequence to Sequence Learning
- **서로 연관된 두 개의 데이터 시퀀스 간의 관계를 모델링하는 방식**
	- 하나의 시퀀스 -> 다른 시퀀스 데이터를 예측,변환하는 모델 제작
	- 입력 시퀀스 -> 적절한 출력 시퀀스
	- 번역, 요약, 음성 인식 등

### 정의
- ==**Sequnce 데이터 사이의 관계를 규명**==
- 입력 -> 출력이 되는 원인과 결과 관계를 두 데이터 사이에서 모델링을 통해 구현하는 학습 방식
	- RNN이든 CNN이든 구현체는 무관
- 이미 구축, 수집된 두 데이터 `x`와 `y`에 대해서 Seq2Seq 모델 훈련
	- 입력 `seq x`에 대해서 출력 `seq y`를 생성

### 구체적 정의
- 입력 시퀀스 `x`, 출력 시퀀스 `y`, 입력 아이템 개수 `N`, 출력 데이터 개수 `M`

![[1__qny2Eqaylu7dqYDCPc0kw.webp]]
1. **Case 1: N과 M이 같은 경우**
	- 시퀀스의 아이탬 개수 `N` = 출력 데이터 개수 `M`
2. **Case 2: N과 M이 다른 경우**
	- **Case N21** : 출력 M이 1인 경우(ex. text classification)
	- **Case N2M**: 시퀀스의 아이탬 개수 `N` =/= 출력 데이터 개수 `M` (ex. 번역 문제)

### 적용 범위

#### 음성 인식
- 과거 음성 인식
	- 음향 모델링, 언어 모델링
	- `음성` -> 음향 모델 -> `단어` -> 언어 모델 -> `다음 단어` 예측
- Seq2Seq
	- `음성 데이터` -> S2S -> `텍스트 데이터`
	- 직관, 효율적으로 본질을 단순화
	- 최신 기술 Whisper도 이를 활용
	- 내부구조 이해 필요 X, 데이터 활용에 집중 가능

#### 영상 처리
- 영상 데이터 내 특정 이벤트 검출
###### 예) 타자의 배트 스윙 영상
- 과거
	- 복잡한 처리 과정
	- 스윙하는 궤적을 분석
- Seq2Seq
	1. 쪼개서 프레임을 하나씩 시퀀스 데이터로 처리
	2. 각 프레임에 해당하는 이미지를 입력
	3. 이미지가 설명하는 이벤트에 대한 라벨을 붙임
	- 즉, **Video Frame** -> **Scene Labels**
	- 라벨링된 데이터로 학습된 모델은 새 영상의 주요 이벤트 시퀀스를 자동으로 생성 가능 
- `입력 영상`, `이벤트 라벨` -> 영상 내 이벤트 검출기 제작 가능

#### 자연어 처리
- **문자, 토큰, 단어** -> 적절한 **태그, 품사**
- 형태소 분석 : 주어진 단어, 단어 시퀀스의 단어가 어떤 품사에 속하는지 매핑
- **언어학적 지식은 필요 X**
	- 적절하게 매핑된 데이터셋 -> 다양한 자연어 처리 도구 쉽게 구현

### 상상을 그대로 구현
- 복잡한 문제를 단순화
- 데이터쌍만 있으면 분야 지식 없이도 모델 구축 가능
- 산수 문제
	- Math Expr. -> Numbers
- 번역
	- Kor Text Seq -> Eng Text Seq
- 문장 자동완성
	- 문장을 나눠서 입/출 `x`-`y` 쌍으로 구성

- ==**주어진 문제를 어떻게 정의하고, 입력(X)과 출력(Y)을 어떻게 설정하느냐가 중요**==
- 구체적인 상상 + 입출력 데이터
- 핵심엔진(구현체)도 진화중
	- RNN, RNN+Attention, Transformer, Mamba


## 딥러닝에서의 Seq to Seq 구현 방법
- 최근에는 Transformer 기반
- 개념적 이해를 위해 전통적 방식을 설명

### 독립적인 접근 방식
- 가장 간단한 접근법
- 각 시퀀스 데이터를 독립적으로 처리
	- `x1, x2, x3, x4`를 각 `xi`에 대해 독립적으로 `yi`를 예측
- 시간적 연속성은 X

### Convolution 아이디어 적용
- 과거 여러 시점의 데이터를 한번에 고려
- 시간적 연속성 어느정도 가능
	- **전체적인 패턴 모델링에는 한계**

### Recurrent Neural Network (RNN)
- 시퀀스 데이터 전체적인 패턴 모델링에 적합
- 과거의 정보 -> 현재의 결정에 반영
	- `x1`에서 `y1`를 예측할 때 생성되는 정보(중간 상태) `h1`
	- `x2`에서 `y2`를 예측할 때 `h1`를 활용해서 `h2 `생성 
- **시퀀스 전체에 걸쳐 연속성, 관련성 유지**

![[1_-O5FKiqCb_a3zBQwvjhPuw.webp]]

#### Vanilla RNN의 문제점
1. **Vanishing Gradient Problem**
	- 시간이 지남에 따라 기울기 작아짐 -> 전달 X
	- 장기 의존성 ↓
2. **Exploding Gradient Problem**
	- 기울기가 너무 커져 불안정
3. **Long-Term Dependencies**
	- 과거의 정보 유지, 활용에 한계
	- 입력 시퀀스가 길어질수록 과거 정보의 영향력 ↓

- RNN은 시간에 따라 정보를 전달하도록 설계
- 긴 시퀀스에서는 중요한 정보 희석/손실의 위험
	- LSTM, GRU의 등장 배경
	- 여전히 긴 시퀀스에서의 **global modeling에는 한계** 있음

- ==**Attention 메커니즘**== -> 근본적 해결 위해 도입
	- 중요한 부분에 주목 -> 필요한 정보 효과적 선택
	- 시퀀스 내 어디에 있든 관련성에 따라 접근
- **Transformer**
	- Attention 메커니즘 근간
	- RNN, LSTM 과는 달리 전체 시퀀스를 한번에 처리
	- 전역적 모델링 ↑, **병렬처리 가능**, 학습 속도 ↑

### 네트워크 구조 선택
- RNN, LSTM, Transformer 등 여러 도구 존재하지만, 다른 유형이나 새로운 구조 개발 가능
- 아키텍쳐 선택 시 고려할 사항
	- 기존 학습된 모델 재활용 여부
	- Inference 속도
	- 처리 데이터의 장기 의존성 포함 여부, 그 범위
	- Inference 실행 환경, 모델이 적합성(메모리, GPU 등)

## RNN을 이용한 Seq to Seq 구현
- Seq2Seq learning은 크게 세 가지 형태
1. Encoding only approach
2. Encoindg - Decoding approach
3. **Decoding only approach**
	- GPT 기술의 근간 -> 추후 설명

### Encoding only approach
- 예시 : RNN 활용 간단한 Seq2Seq 기반 intent detection 구현
	- 토큰, 단어의 시퀀스 -> intent label

- N21과 N2N 문제는 Encoding 만으로 쉽게 접근 가능

#### N2N 문제
- 예) RNN을 활용한 품사 태깅
	- 단어, 토큰 시퀀스 -> 품사 시퀀스

![[RNN_N2N.webp]]

- **데이터 모델링**
	1. `토큰` -> one-hot-encoding -> Lookup Table -> `dense-vector`
	2. `dense-vector` -> RNN -> 품사 label에 해당하는 one-hot 벡터로 매핑 -> `품사`
- Lookup Table은 다른 방식 사용 가능, RNN layer도 추가 가능

#### N21 문제
- N개의 데이터의 요약, 추상화, 핵심 정보는 어디에?
	- RNN은 과거의 중요한 정보들을 미래까지 전달
- **RNN의 마지막 벡터에 모든 정보가 담김**
- 마지막 벡터를 통해 **입력 시퀀스 전체를 추상화한 숫자**를 얻음
- 자연어 처리, 음성 데이터 -> 스피치 인코딩, 비디오 프레임 ->비디오 인코딩
- RNN 활용 : **==시간에 따라 변화하는 다양한 데이터를 효과적으로 모델링, 인코딩==**
	- 매우 직관적, 다양한 분야에 응용
- 자연어 처리의 목표 : **문장 전체를 정확히 파악하여 의도를 파악**

![[RNN_N21.webp]]
- `토큰` -> Lookup Table -> `dense` 형태 -> RNN -> 출력 하나
- Seq2Seq는 **엔드 투 엔드** 지향
	- 내부 메커니즘 걱정없이 전체 프로세스 모델링
	-  입-출력 적절한 설계로 다양항 응용 개발 가능

### Encoding + Decoding Approach
- 인코딩된 벡터를 복사, 다른 RNN에 입력으로 사용
	- 인코딩에 사용된 RNN과는 다름
- 1번 RNN에서 인코딩된 벡터를 복사해서 2번 RNN에 입력으로 주고 디코딩
	- N2M 문제를 해결 가능

- 산술 연산도 N2M으로 구현 가능
	- 구체적인 알고리즘 없이도 스스로 학습, 문제 해결
	- 결과 : 세 자리 + 패딩
	1. 수식 -> RNN -> 수식의 퀀스
	2. 벡터 -> RNN -> 수식의 결과물
	![[NtoM_Cal.webp]]

## 정리
- Seq 2 Seq 프레임워크로 다양한 문제 해결 가능
- 깊은 신경망 지식 없이도 충분한 양의 입력/출력 데이터 -> 머신러닝 모델 구현 가능