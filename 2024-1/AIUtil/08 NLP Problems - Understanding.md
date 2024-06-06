- 기계의 언어 **이해/해석/추론 능력**을 파악, 평가
- AI 모델이 얼마나 **언어와 문화를 잘 이해**하는지 측정
- **기반 모델로서 잠재력 평가**

#### 언어 이해 능력 중심 벤치마크
- **GLUE**
	- 다양한 NLP 작업 포함, 종합적 언어 이해 능력 평가
	- 자연어 추론, 감정 분석, 문장 유사성 평가
- **SuperGLUE**
	- 더 어려운 NLP 작업 포함, 이해 능력 깊게 평가
	- 복잡한 추론 질의응답, 세밀한 감성 분석

#### LLM 특화 벤치마크
- **BIG-bench**
	- Google이 발표
	- 창의성, 상식, 언어 추론 등 테스트
- **Hugging Face’s Model-Eval**
	- Hugging Face에서 제공
	- 포괄적 평가 도구 제공
	- 언어 이해 능력, 번역 능력, 특정 테스크 성능 측정
- **Dynabench**
	- Facebook AI Research가 개발
	- 모델을 동적으로 평가, 오류 포인트 파악

### GLUE (General Language Understanding Evaluation)
- GLUE 벤치마크의 NLP 작업

### Super GLUE
- GLUE 보다 더 어려운 작업으로 구성

### 문제 모델링
- 거의 모든 문제가 `N 토큰` -> `1개 숫자/클래스 라벨`
	- 다양한 형태의 text 입력 -> 간단한 출력
- **N21** 문제로 모델링 가능
	- **생성형 X, BERT 같은 transformer 인코더 계열 모델이 적합**

- 한 문장 입력
	- **`CoLA` 태스크** : 가능한 문장인지

- 두 문장 입력
	- **`MRPC` 태스크** : 두 문장이 Paraphrase 관계인지