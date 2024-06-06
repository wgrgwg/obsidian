- `<!DOCTYPE html>`
	- 문서의 HTML 버전을 지정
	- 표준 HTML5

- `<html></html>`
	- 시작, 종료 태그
	- 문서의 전체 범위를 의미

- `<head></head>`
	- 문서의 정보를 나타내는 범위
	- 제목, 설명, 사용할 파일 위치, 스타일
	- **보이지 않는 정보**를 작성
	- `<title>제목</title>` 웹페이지의 제목
	- `<link rel="stylesheet" href="./main.css">`
		- 외부 문서를 가져와 연결
		- css 파일 연결
		- `favicon` : 대표 아이콘
	- `<style></style>`
		- 스타일을 HTML 문서 안에서 작성
	- `<script src="./main"><script>`
		- JS 파일 연결
		- JS 문법도 작성 가능
	- `<meta/>` HTML 문서의 제작자, 내용, 키워드 같은 여러 정보를 검색엔진이나 브라우저에게 제공
		- `charset` 문자 인코딩 방식
		- `name`, `content` 정보의 종류, 값

- `<body></body>`
	- 문서의 구조를 나타내는 범위
	- 로고, 헤더, 푸터, 내비게이션, 메뉴, 버튼, 이미지, ...
	- 사용자 화면을 통해 **보여지는 구조**

- `<script src="./main"><script>`
	- js 파일 연결

- 화면에 이미지 출력
	- `<img src="./images/download.jpg" alt="inside_out">`

- **상대 경로**
	- `./` (생략 가능)
	- `../` 상위 폴더

- **절대 경로**
	- `http` or `https` 원격의 사이트 주소
	- `/` or `//`

- `http://localhost:5500`
	- 로컬 환경
	- 5500 주소
	- 루트 경로의 `index.html`

- css 이미지 출력
	- `background: url(주소)`도 가능

- 페이지를 나누고 연결(링크)
	- `<a href="주소"></a>`
	- 주소 기본값은 해당 경로의 `index.html`
	- `<a href="/">Home</a>`
		- 루트 경로의 index.html로 이동

- 개발자 도구 사용하기
	- Elements
		- CSS 구조 분석 가능
		- Styles : CSS 선언 가능
	- console

- 웹에서 코딩
	- `codepen.io`
		- head 부분은 생략

- 브라우저 스타일 초기화
	- `reset.css` cdn
	- `reset.min.css` 경량화(추천)

- emmet
	- `tab`키로 태그 자동완성

### HTML 기본 문법
- `<태그>내용</태그>
	- 요소(Element)
	- 내용에는 다른 요소 삽입 가능 - **자식**

- **부모-자식** 요소
	- 들여쓰기(indent)로 가시화

- `<태그/>` or `<태그>`
	- 빈 태그 (닫는 태그 따로 X)

- `<태그 속성="값">내용</태그>`
	- `<img src= "주소" alt = "대체텍스트" />`
	- 빈 태그엔 주로 속성+값이 추가
	- 필수 속성도 존재

- **인라인 요소** : 글자를 만들기 위한 요소들
	- `<span></span>` 컨텐츠 영역을 설정
		- 줄바꿈 시에 space 생김
	- 수평으로 쌓임
	- width, height 설정 불가
	- 여백은 좌우는 가능(margin, padding)
	- 자식으로 블록 요소는 불가
	
- **블록 요소** : 상자(레이아웃)를 만들기 위한 요소들
	- 수직으로 쌓임
	- **부모 요소의 크기만큼 자동으로 늘어남(가로)**
	- width, height 지정 가능

- `<div></div>`
	- 특별한 의미가 없는 구분을 위한 block 요소

- `<h1></h1>`
	- 숫자로 중요도 의미
	- 제목을 의미하는 block 요소

- `<p></p>`
	- 문장을 의미하는 block 요소

- `<img/>`
	- 이미지 삽입하는 inline 요소
	- 필수 속성 : `src`, `alt`

- `<ul></ul>`
	- 순서가 필요없는 목록의 집합 (block)

- `<li></li>`
	- 목록내 각 항목 (block)

- `<a></a>`
	- 다른/같은 페이지로 이동하는 하이퍼링크 지정 요소 (inline)
	- **`href` 속성으로 경로를 명시**

- `<br/>`
	- 줄바꿈 요소 (inline)

- `<input/>`
	- 사용자가 데이터 입력
	- inline-block 요소
	- inline이지만 가로/세로, 여백 설정 가능
	- `type` 데이터의 타입
		- `checkbox` 타입 - `<label></label>`로 input과 텍스트 묶기
			- checked - 미리 체크
		- `radio` 타입 - 그룹 중 하나만 체크
			- `name`으로 그룹화
	- `value` 미리 데이터 입력
	- `disabled` 입력 요소 비활성화

- `<table></table>`
	- 행 - row `<tr></tr>`
	- 열 - column `<td></td>`

- `<!--주석 내용-->`
	- 화면에 출력 X

### 전역 속성
- `title=""`
	- 커서 올릴 시 표시
	- 요소의 정보나 설명을 저장

- `style=""`
	- 요소에 적용할 스타일(CSS)을 지정

- `class=""`
	- 요소를 지칭하는 **중복가능한 이름**

- `id=""`
	- 요소를 지칭하는 **고유한 이름**

- `data-이름="데이터"`
	- 요소에 데이터를 지정(text)
	- 데이터는 JS에서 사용 가능
	- `script`의 `defer` 속성
		- html 읽은 후 JS


