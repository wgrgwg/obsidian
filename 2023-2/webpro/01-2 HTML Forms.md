## Form
- `<form>` : input element들을 위한 컨테이너, action, method, target 속성 가짐
	- `<form action="/action_page.php" target="_blank" method="get">`
	- `action` : 보내는 링크 
	- `taget` : 응답 형태
		- `_blank` : 새 창에 표시
		- `_self`  : 같은 프레임에 표시
		- `_parent` : 부모 프레임에 표시
		- `_top` : 창 전체에 표시
		- `framename` : iframe 이름으로 지정
	- `method` 
		- `get` : url에 찍힘
		- `post` : http request body로 보냄
- `<input>` : type 속성
	- `text`
	- `radio` : 하나 필수 선택
	- `checkbox`
	- `submit` : form 제출
	- `button`
- `<label>` : input 값
	- for 속성으로 input 엘리먼트 id 지정
- `<select>` : 드롭다운 리스트
	- `<option>`으로 요소 지정
```html
<select id="cars" name="cars">
    <option value="volvo">Volvo</option>
    <option value="saab">Saab</option>
    <option value="fiat">Fiat</option>
    <option value="audi">Audi</option>
  </select>
```