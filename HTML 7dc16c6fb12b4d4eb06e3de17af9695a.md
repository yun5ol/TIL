# HTML

## HTML

- “**Hyper Text** (고도화된 텍스트)”
    
    고도화를 위해 별도의 **표시** (형식) 이 필요 = **Markup** > **L**anguage 필요하여 탄생한
    
    **고도화된 마크업 언어 : HTML** 
    

- 웹에서 자유롭게 오갈 수 있는 웹 문서를 만드는 언어

# 태그 정리

---

### 문서의 기본 구조

```html
<!doctype html> 
현재 문서가 HTML5 언어로 작성한 웹 문서이다.
항상 맨 첫째줄

<html>~</html>
웹 문서의 시작과 끝을 나타내는 태그이다.

<head>~</head>
웹 브라우저가 웹 문서를 해석하는 데 필요한 정보를 입력하는 부분이다.
헤드 부분은 웹 브라우저에 나타나지 않는다.

<body>~</body>
실제로 우베 브라우저 화면에 나타나는 내용.
주 태그들은 <body> 태그 안에 존재한다.

문서의 정보를 지정하는 <meta> 태그
한글로 된 내용을 표시하기 위해서 UTF-8 문자 세트를 사용
<meta charset=:UTF-8">
그 외
<meta name="keyword" content="html의 구조">

문서 제목을 나타내는 <title> 태그
<tiltle> HTML 기본문서 </title>
```

### 웹 브라우저에 내용을 표시하는 <body> 기본 태그

```html
<h1></h1>
# 제목. 1~6 까지

<p></p>
# 단락 나눔 pragraph

<em></em>
# 강조: 이탤릭체 emphasize

<strong></strong>
# 강조 : 볼드체

<b></b>
# 볼드체, strong 은 강조의 효과가 있고 b는 볼드만!

<br>
# 줄 바꿈 break, 닫는태그 없음

<hr>
# 가로줄, 닫는태그 없음

<ol>,<ol>
# 순서가 있는 목록 ordered list
 <li></li>
 # 각 항목에 달아줌
	<ol type=1> <ol type=a>
 # 순서 규정
<ul></ul>
# 순서가 없는 목록 unordered list, bullet 으로 표시됨
```

### 표 구성 태그

```html
<table>
# 표 생성
<caption></caption> 표 제목
<tr></tr> 행 table row
<th></th> 표 제목 table head
<td></td> 표 데이터 table data
```

### 이미지 / 오디오 / 비디오

**파일의 “경로” 중요**

```html
<img src="images/tangerlines.jpg" alt="레드향">
# alt 대체텍스트 : 시각장애인에게 내용을 읽어주는 용도
아이콘 처럼 특정한 데이터가 아닐 경우 빈칸으로!

<audio src="medias/spring.mp3" controls></audio>
# alt 없음
# controls : 재생버튼

<video src="medias/salad.mp4" controls width="450"></video>
# alt 없음
# controls : 재생버튼
# width=:450" 크기 지정 가능

<audio, video 태그의 속성>
controls 재생 버튼
autoply 자동 재생
loap 반복 재생
muted 무음, 자동 재생이 가능
preload 페이지를 불러올 때 오디오나 비디오 파일을 어떻게 로딩할지 지정
width,height 사이즈 지정
poster="파일 이름" 비디오에만, 비디오가 재생되기 전까지 화면에 표시될 포스터 이미지 지정
```

### 하이퍼링크

```html
<p><a href="embed.html">멀티미디어 삽입하기</a></p>
# 텍스트파일 하이퍼링크

<a href="index.html"><img src="images/tangerlines.jpg" alt="레드향"></a>
# 이미지파일 하이퍼링크

<속성>
target="_blank" 새 창에서 열기
```

### 폼 삽입하기 input type =””

폼이란, 웹에서 사용자의 정보를 받아들이기 위한 입력 형식

정보를 입력 받아 서버로 보내줄 뿐 데이터를 직접 처리하진 않는다.

eg. 검색창, 로그인창, 계정생성 팝업창

```html
<form action=""> 서버에서 데이터를 처리할 프로그램 지정 
  <label>아이디 : <input type="text"></label> 입력필드와 항목을 구분
  <label>비밀번호 : <input type="password"></label>
</form>
  <input type="submit" value="전송"> value 값으로 아이콘 표시

# <label> 은 아래처럼 따로 표기도 가능
  <lable for="user-id">아이디 : </label>
	<input type-"text" id="user-id">

# type="radion" type="checkbox"
	<input type="radio" name="cf"/>짜장면   radio button 1가지만 선택 가능
  <input type="radio" name="cf"/>짬뽕    checkbox 2 이상 선택 가능
  <input type="radio" name="cf"/>짬짜면  name 동일 그룹임을 표시
	<input type="checkbox" />정보처리기사  checkbox 2 이상 선택 가능
  <input type="checkbox" />운전면허
  <input type="checkbox" checked/>오라클자격증

# type="number" type="range"
	<input type="number">
	<input type="range">

<속성>
min 최소값
max 최대값
value 화면에 표시되는 초기값

# type="date" type="time"
	<input type="date">
	<input type="month">
	<input type="weak">
  <input type="datetime">
  <input type="datetime-local">

# type="hidden"
  <input type="hidden" value="okok">
유저가 직접 입력하진 않지만 전송과 함께 전달 됨
eg. 가입 경로, 검색 경로 etc...
```

### input 태그의 주요 속성

```html
# required 속성
누락된 기입 정보를 다시 고지시켜줌
	<lable for="user-id">아이디 : </label>
	<input type-"text" id="user-id" required>

# readonly 속성
사용자가 수정, 기입 하지 못함, 읽기 전용
  <lable for="user-id">아이디 : </label>
	<input type-"text" id="user-id" readonly>

# autofocus 속성
커서가 순서에 맞게 해당 필드에 자동 위치함
	<lable for="user-id">아이디 : </label>
	<input type-"text" id="user-id" required autofocus>
```

### input 외 폼 태그

```html
# textarea
<form>
  <textarea id="memo" cols="40" rows="4"></textarea> 화면에 보이는 칼럼(글자)수와 행수 대략 설정
</form>

# selectmenu
여러 항목 중 한 가지 고르도록
<select>
  <option value="1줄">김밥 1줄</option>  셀렉트메뉴에 들어가는 항목 태그  
  <option value="1인분">떡볶이 1인분</option>  서버로 넘어가는 정보 유저에게 보이는 정보
  <option value="2인분" selected>순대 2인분</option> 자동 추가될 항목
  <option>오뎅</option>
</select>
```