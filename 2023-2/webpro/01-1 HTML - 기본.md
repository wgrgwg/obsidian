# HTML 기본문법
## 기본 페이지 구조
```html
<!DOCTYPE html>
<html lang="ko">

<head>
	<meta charst="utf-8">
	<title>html 기본 구조</title>
</head>
	
<body>
	<h1>제목1</h1>
	<p>본문1</p>
</body>

</html>
```

## 태그들
### 하이퍼링크
- `<a>` : text에 링크 거는 태그
	- href : 링크 값 갖는 속성
	- target : 문서가 열릴 위치 명시
		- `_blank` : 새로운 윈도우나 tab 
		- `_self` : 현재 프레임에 오픈(기본값)
		- `_parent` : 부모 프레임
		- `_top` : 현재 윈도우 전체 
	- `<a href="http://www.w3schools.com">Visit W3Schools</a>`
	- **경로는 상대경로로**

### 이미지
- `<img>` : 이미지 태그
	- 닫는 태그 없음
	- src : 이미지 주소
	- alt : 대체 메시지
	- 사이즈는 style 속성으로 정의 가능
	- `<img src="img_girl.jpg" alt="Girl with a jacket" style="width:100px;height:200px;">` 

### 기타
- `<h1></h1>` ~ `<h6></h6>` : 제목 태그
- `<hr>` :  수평선
- `<br>` : 개행
- `<pre>` : 텍스트 서식 유지
- `<iframe>` : 다른 page 삽입
	- `<iframe src="url" title="description"></iframe>` 

### 텍스트 관련 태그
- `<b>` : bold
- `<strong>` : 강조
- `<i>` : 이탤릭
- `<em>` : 강조
- `<mark>` : 형광펜
- `<small>` : 작은 문자
- `<del>` : 취소선
- `<ins>` : 밑줄
- `<sub>` : 아랫첨자
- `<sup>` : 윗첨자

### 테이블
- `<tr>` : 테이블 한 행
- `<th>` : 테이블 헤더
- `<td>` : 테이블 일반 내용
테이블 테두리 단일선 : style `border-collapse: collapse;` 값을 줌
행,열 병합
	- 가로 병합 : 속성을 `colspan = "2"`
	- 세로 병합 : `rowspan = "2"`

### 주석
`<!-- 주석입니다. -->` 

### 리스트
- `<ul>` : 정렬 안된 리스트
- `<li>` : 리스트 내부 내용
- `<ol>` : 정렬된 리스트
	- type 속성으로 모양 지정 가능
	- `type="A"` 알파벳 넘버링(대문자)
	- `type="i"` 로마자 넘버링(소문자)


## Block and Inlien Elements
- **Block**
	- 블럭 단위로 전부 차지
	- 리스트는 block
- **Inline**
	- 딱 지정된 영역만
	- `<span>` 대표적