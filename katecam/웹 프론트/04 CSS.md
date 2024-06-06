### CSS
- `선택자 { 속성: 값; }`
	- 선택자(Selector) - CSS를 적용할 대상
	- 속성 - CSS의 종류(Property)
	- 값 - CSS의 값(Value)
	- 속성은 값이다
- 예) `div { color: red; }`
	- div 내부의 글자들의 색을 red로 설정
- 주석
	- `/* 설명 작성 */`

#### CSS의 선언 방식
1. **내장 방식**
	- `<style></style>`의 내용으로 스타일 작성
2. **인라인 방식**
	- 요소의 **style 속성**에 직접 스타일 작성(선택자 X)
	- `<div style="color": red; margin: 20px;"></div>`
	- 우선순위 최고
3. **링크 방식**
	- `<link rel="stylesheet" href="./css/main.css">`
	- 병렬 방식
4. **import 방식**
	- CSS의 @import 규칙으로 CSS 문서 안에서 또 다른 CSS 문서를 가져와 연결하는 방식
	- `@import url("./box.css");`
	- 직렬 연결
		- 지연 연결
		- 연결을 의존

#### CSS 선택자
- 선택자 유형
	- 기본
	- 복합
	- 가상 클래스
	- 가상 요소
	- 속성

##### 기본
- `*`
	- 기본, 전체 선택자
	- 모든 요소를 선택

- `태그명`
	- 기본, 태그 선택자

- `.클래스명`
	- 기본, 클래스 선택자
	- HTML class 속성의 값이 `클래스명`인 요소 선택

- `#id명`
	- 기본, 아이디 선택자
	- HTML id 속성의 값이 `id명`인 요소 선택

##### 복합
- `ABC.XYZ`
	- 복합, 일치 선택자
	- 선택자 ABC와 XYZ를 동시에 만족하는 요소 선택

- `ABC>XYZ`
	- 복합, 자식 선택자
	- ABC의 자식 요소 XYZ 선택
	- `ul > .orange{ color: red; }`
		- ul의 자식인 orange 클래스

- `ABC XYZ`
	- 복합, 후손 선택자
	- 선택자 ABC의 하위 요소 XYZ 선택
	- `div .orange { color: red; }`

- `ABC + XYZ`
	- 복합, 인접 형제 선택자
	- 선택자 ABC의 다음 형제 요소 XYZ **하나**를 선택

- `ABC ~ XYZ`
	- 복합, 일반 형제 선택자
	- 선택자 ABC의 다음 형제 요소 XYZ **모두**를 선택

##### 가상 클래스
- `ABC:hover`
	- 선택자 ABC 요소에 **마우스 커서가 올라가 있는** 상태
- `ABC:active`
	- 클릭중인 상태
- `ABC:focus`
	- ABC요소가 **포커스**되면 선택
	- 값 입력받는 경우(커서 활성화)

- `ABC:first-child`
	- 선택자 ABC가 **형제 요소 중 첫째**라면 선택
- `ABC:last-child`
	- 선택자 ABC가 **형제 요소 중 막내**라면 선택
- `ABC:nth-child(n)`
	- 선택자 ABC가 **형제 요소 중 `n`째**라면 선택
		- `2n` : 짝수번
- `ABC:not(XYZ)`
	- 선택자 XYZ가 아닌 ABC라면 선택
- `ABC::before`
	- 선택자 ABC 요소의 내부 앞에 내용을 삽입
	- `.box::before { content: "앞!"; }`
	- after -> 뒤에 삽입

##### 속성
- `[ABC]`
	- 속성 ABC를 포함한 요소 선택
- `[ABC="XYZ"]`
	- XYZ 값을 갖는 속성 ABC를 포함한 요소 선택

##### 상속
- 부모 요소의 속성이 하위 요소에 적용
	- 글자 스타일, 폰트, 정렬 등
	- 모든 건 아님 X
- 강제 상속 
	- `inherit` 부모의 속성을 강제 상속

##### 우선 순위
- 어떤 선언의 CSS 속성을 우선 적용할 지 결정
	1. 점수가 높은 선언이 우선
	2. 점수가 같으면, 마지막 해석된 선언이 우선
- `!important` -> 우선도 매우 중요