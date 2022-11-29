# 🖌 CSS 사용법 (2)

📗 교재: Do it! 웹표준의정석  
🏷 태그: Dev, 웹&모바일, 웹프로그래밍기초  
📆 학습일: 11/29/2022  

## 1. CSS (2)

### 1.1 border 테두리

```css
5-1 # border

#menu {
    border-style: solid;
    border-width: 1px;   /*모든 테두리!*/
    border-color: red;
  }

#footer { /* border의 style, width, color를 한 번에 지정할 수 있다*/
    border: 4px red solid; /* 값을 지정하는 순서는 상관없다.*/
  }

#content {   /* border별 스타일을 달리 */
    border-top-width: 2px;
    border-top-style: dotted;
    border-top-color: blue;
    border-bottom: dashed 4px orange;
    border-left: solid 6px green;
    border-right: red dotted 40px;
  }

아래쪽으로 갈 수록 우선순위가 높은게, 유지보수상 좋다!
```

```css
5-2 # padding

body {
    border: 5px solid red;
    /* 모든 방향 */
    padding: 10px; 
    margin: 0px;
  }
  
  /* 안쪽 여백 주기*/
  div {
    border: 2px solid gray;
  }

  h1, ul {
    border: 1px solid red;
    margin: 0px;
  }

  #menu {
    padding-top: 10px;
    padding-right: 20px;  /*패딩 별 사이즈 설정*/
    padding-bottom: 30px;
    padding-left: 40px;
  }

  #content {
    /* 순서 => 시계 침이 도는 방향(12, 3, 6, 9)*/
    padding: 10px 20px 30px 40px; 
  }

  #footer {
    /* 순서: (top/bottom) (left/right)*/
    padding: 10px 50px; 
  }
```

```css
5-3 # 바깥쪽 여백 주기 

body {    /* 0픽셀 단위 생략 가능 */
    border: 10px solid blue;
    margin: 0;
    padding: 0;
  }
  ...
  a {
    border: 1px solid red;
    margin: 10px;
    height: 30px;
    width: 120px;
    display: inline-block;    */ 인라인 태그는 마진이 좌우는 먹히나, 상하는 x /*
  }                        */너비도 콘텐츠 너비로 결정됨, 그래서 설정한 게 inline-block /*  
...
```

```css
5-4 # 태그 너비와 높이
 /* content-box(기본)
      => width = 콘텐츠 너비
      => height = 콘텐츠 높이
    border-box
    => width = 콘텐츠너비 + 좌,우 패딩너비 + 좌,우 테두리너비
    => height = 콘텐츠높이 + 위,아래 패딩높이 + 위,아래 테두리높이 */

...
  div {
    border: 10px solid red;
    margin: 10px;
    background-color: blue;
    color: white;
    width: 200px;  /* 콘텐츠의 너비, 패딩 포함x */
    height: 100px;  /* 콘텐츠의 높이, 패딩 포함x */
  }  

  #menu {
    border-left-width: 50px;
    padding-left: 30px;
  }
  
  #content {
    background-color: gray;
    /* border-box 라고 설정하면 width, height는 
       콘텐트 크기가 아니라 박스 크기가 된다. */
    **box-sizing: border-box;    /*디폴트로 쓰자*/**
    margin-left: 20px;
    border-left-width: 50px;
    padding-left: 30px; /*패딩이 더해져도 width는 콘텐츠의 너비이므로 그대로 */
  }

#footer {
    background-color: yellow;
    border-width: 1px;
    box-sizing: border-box;
  }
```

### 1.2 font 폰트

**Raster 폰트** : 픽셀 단위로 글자를 만든다. (비트맵 폰트)

+ 출력 속도가 빠르다.

    이미지의 복잡도와 상관없이 파일크기(해상도)가 동일하다.

-  폰트 크기에 따라 각 문자를 만들어야 한다.

    정해진 크기보다 크게 출력하면 단순히 각 픽셀의 크기를 늘리기 때문에, 계단 현상이 발생한다.

⬇

**Vector 폰트** : 글자를 그리는 명령어를 작성한다. 

글자를 그리는 명령을 수행하므로,

- 출력 속도가 느리다. (raster 대비. 요즘은 cpu가 빨라서 무관)

   이미지 복잡도에 따라 파일크기(해상도)가 달라진다. (다만, 이미지가 단순하면 극단적으로 작아진다.)

+ 글자 크기를 늘리더라도 명령을 통해 그리기 때문에, 계단 현상이 발생하지 않는다.  

```css
6-1 # 폰트 다루기
/*  => font-family : 폰트 그룹
       예) sans-serif(고딕체), serif(명조체), monospace(고정너비),
           cursive(흘림체), fantasy
    => font : 폰트 그룹에 속해 있는 폰트
       예) sans-serif => 맑은 고딕, 돋움체, 굴림체, Arial 등
           serif => 궁서체, 바탕체, Times 등
           monospace => monaco, consolas, Currier New 등
           cursive => 나눔 손글씨, 필기체 등
  */

#menu {
    font-family: '맑은 고딕', 굴림체, 'Apple SD Gothic Neo', sans-serif;
    /* 의미
       => 맑은 고딕 폰트를 사용하라. 없다면 다음 폰트 사용하라.
       => 모두 없다면 웹브라우저에 설정된 sans-serif 기본 폰트를 사용하라.
			 => 폰트에 띄어쓰기가 있으면 ' ' 안에 작성 할 것
     */
  }
```

```css
6-2 # 폰트 크기 설정

body {
    font-size: small; 
  }    /* font-size
       미리 정의된 값: xx-small, x-small, small, medium, large, x-large, xx-large
       숫자로 값(폰트의 높이)을 지정할 수 있다. 예) 20px
       보통 small을 많이 사용한다.*/ 

#menu {
    font-family: '맑은 고딕', 굴림체, 'Apple SD Gothic Neo', sans-serif;
    xfont-size: 30px;
    /* 실무에서는 유지보수를 쉽게 하기 위해 
       body 태그에 설정한 기본 폰트 크기를 기준으로 **비율**로 지정한다. */
    xfont-size: 1.2em; /*정의값 small의 1.2배*/    /*px 또는 em(배수) 또는 % 또는 정의값으로 설정*/
    font-size: 150%;
  }

6-3 # 폰트 크기 설정 (2)

/* 폰트 크기 II
    => 폰트 크기를 특정 숫자로 고정을 시키면
       유지보수할 때 폰트의 크기를 변경하기가 번거로워진다.
       모든 스타일을 다 변경해야 하기 때문이다.
    => 실전!
       폰트는 자동으로 자식 태그에게 상속하는 스타일이기 때문에
       body에서 font-family를 지정한다.
       그리고, body에 폰트 크기를 지정한 다음,
       나머지 태그에 대해서는 상대 크기를 지정한다.
    => font-size 상대 크기를 지정하는 문법
       몇 배수인지 지정 => 2.4em
       %로 지정         => 240%
  */
```

```css
6-4 # 폰트 기타 속성
/* => font-weight
       폰트의 두께 지정
    => font-style   처음부터 기울어진 폰트   실시간으로 기울이기
       폰트의 모양 지정. 예) italic, normal, oblique
  */

#footer > p {
    font-family: D2Coding, serif;
    font-style: oblique;
    /* italic => 폰트 파일에 있는 이탤릭체를 사용한다.  그냥 이탤릭을 선호하자!
       oblique => 운영체제가 폰트를 강제로 기울여서 이탤릭체처럼 보이게 한다.
                  폰트 파일에 이탤릭체가 없을 때 사용한다.
    */
  }
```

### 1.3 텍스트 꾸미기

![image](https://user-images.githubusercontent.com/118426836/204509842-d31f0eab-cce3-4e4b-ad63-24764ad880d9.png)


float: left;

```css
6-5 # 텍스트 꾸미기
 /* => text-decoration
    => text-align
  */

address {  /*기본이 블록 타입이다*/
    /* border: 1px solid blue; */
    display: inline;
    font-style: normal;
  }
...
#menu {
    background-color: lightgray;
    font-size: 1.2em;
    width: 180px;
    padding: 10px;
    box-sizing: border-box;
    float: left;   /* 다른 div 위에 공종부양 : left/right 만 있다. */
    margin: 20px;  
  }
...
#footer {
    border: 1px solid red;
    font-size: 80%; 
    /* 왼쪽에 이 태그의 내용을 가리는 것이 있다면 
    그 아래로 위치하도록 이동시킨다.*/
    clear: left;
    text-align: center;  /*가운데 정렬*/
    padding-top: 20px;
    background-color: gray;
    color: white;
  }
```

### 1.4 배경 꾸미기

```css
7-1 # 배경색 지정
/* 배경 색상 지정하기(background-color)
    => 미리 정의된 상수 값: aqua, black, white, gray 등
       예) wikipedia의 web color 참고
    => rgb(%, %, %): rgb(100%, 0%, 0%), rgb(0%, 0%, 100%)
    => rgb(0~255,0~255,0~255): rgb(255,0,0), rgb(0,0,255)
    => #RRGGBB : #FF0000(=#ff0000), #0000FF(=#0000ff)
    => #F56 : #FF5566의 단축 표현법
  */

7-2 # 배경 그림 지정하기(background-image)

    => url('이미지파일의 URL')
 

7-3 # 배경 그림 채우는 방법(background-repeat)

    => repeat(기본 방식으로 X,Y 축 모두 채운다),
       repeat-x(X 축으로만 채운다), repeat-y(Y 축으로만 채운다),
       no-repeat(반복하지 않는다)

7-4 # 배경 위치 조정(background-position)

    => left/right top/bottom
    => left top을 기준으로 위치 이동
       -50px(왼쪽으로 50px 이동) 100px(아래로 100px 이동)
 
div {
    border: 1px solid #5f6;
    padding: 20px;
    margin: 10px;
    width: 200px;
    height: 200px;
    background-image: url('img02.png');  /*일반 img src 하지마*/
    background-repeat: no-repeat;
    float: left;
  }
...
d8 {
    border: 20px dashed gray;
    background-position: -40px 50px;   /*기본이 left, top*/
  }

7-5 # 배경 크기 조정(background-size)

    => 50%(너비) 200%(높이) : 현재 태그의 너비나 높이에서 해당 비율을 점유하기
    => 50%(너비) : 너비를 기준으로 그림의 원래 비율에 맞춰 높이를 자동 계산하기
                   원래 그림의 비율을 유지하기 때문에 그림이 찌그러지지 않는다.
    => 50px(너비) 100px(높이) : 직접 수치를 지정할 수 있다.
    => 50px(너비) : 높이는 그림 비율에 따라 자동 계산된다.
    => 50%(너비) 100px(높이) : %와 px을 섞을 수 있다.
 

7-6 # 배경 크기 조정(background-size)

    => 50%(너비) 200%(높이) : 현재 태그의 너비나 높이에서 해당 비율을 점유하기
    => 50%(너비) : 너비를 기준으로 그림의 원래 비율에 맞춰 높이를 자동 계산하기
                   원래 그림의 비율을 유지하기 때문에 그림이 찌그러지지 않는다.
    => 50px(너비) 100px(높이) : 직접 수치를 지정할 수 있다.
    => 50px(너비) : 높이는 그림 비율에 따라 자동 계산된다.
    => 50%(너비) 100px(높이) : %와 px을 섞을 수 있다.
 

7-7 # 배경 그림을 여러 개 설정하기(background)
 
  body {
    height: 300px;
    border: 2px solid red;
    background: url('img02.png') no-repeat left top,
                url('img01.jpeg') no-repeat left 80px top 20px;
    background-size: 100px 50px, auto 50px; 
    /* 값을 한 개 주면 그 값을 모든 이미지에 적용한다.
    각각의 이미지에 너비를 지정하고 싶다면,
    이와같이 콤마(,)를 사용하여 지정하라! */

7-8 # 배경 응용

<script>  /*자바스크립트 배워야 쉬워요 ㅠㅠ*/
// DOM API를 이용하여 이메일 입력 상자를 알아낸다.
var email = document.getElementById('email'); /*이메일이 있는 태그를 찾아 리턴되는건 이메일*/
var btn = document.getElementById('signupBtn'); /*사인업버튼이 있는 태그를 찾아 리턴되는건 버튼*/

// 사용자가 버튼을 클릭하는 사건(event)이 발생했을 때
// 호출될 함수(event listener = event handler = callback)를 등록한다.
btn.addEventListener('click', function() {
  // 입력 상자에 들어있는 값을 검사하여 이메일 중복 여부에 따라
  // 아이콘을 출력한다.
  if (email.value == "hong@test.com") { /* 존재하는 사용자일 경우*/
    email.style["background-image"] = "url('no.jpeg')";
  } else {
    email.style["background-image"] = "url('ok.jpeg')";
  }

7-9 # 배경 응용 II (네이버에서 쓰는 법)
하나의 이미지 파일에서 위치 조정하여 아이콘 등록

    => bullet 아이콘 컬렉션 파일에서
       배경 그림의 위치를 조정하여 원하는 bullet 아이콘을 출력하는 방법

// 사용자가 버튼을 클릭하는 사건(event)이 발생했을 때
// 호출될 함수(event listener = event handler = callback)를 등록한다.
btn.addEventListener('click', function() {
  // 입력 상자에 들어있는 값을 검사하여 이메일 중복 여부에 따라
  // 아이콘을 출력한다. 
  if (email.value == "hong@test.com") { // 존재하는 사용자일 경우
    state.style.backgroundPosition = "-204px -1px";
    meassageSpan.innerHTML = "중복된 이메일입니다.";
  } else {
    state.style.backgroundPosition = "-167px -1px";
    messageSpan.innerHTML = "사용할 수 있는 이메일입니다.";
  }

7-10 # 배경 응용 III (트위터에서 쓰는 법)
    => bullet 아이콘 폰트 파일을 이용하여 아이콘 출력하기
    => 장점
       폰트이기 때문에 출력 속도가 빠르다.
       색깔을 변경하기 쉽다.
    => 단점
       폰트이기 때문에 단색만 가능하다.
 
  /* 웹에서 다운로드 하는 폰트는 별도로 선언하고 써야 한다.*/
  @font-face {
    font-family: "myfont"; /* 폰트 그룹명을 설정한다. */
    src: url('icons.woff') format('woff');  /*폰트에 이름을 붙인다*/
  }   /*폰트를 전체를 올리는게 아니다*/ 
#state {
    border: 1px solid red;
    font-family: myfont; /* OS에 설치된 폰트가 아니라 외부에서 다운받은 폰트, 그룹명을 쓴다*/
    position: relative;
    top: 3px;
    display: inline-block;
    width: 16px;
    height: 16px;
    margin-left: 2px;
    font-size: 20px;
  }
...
<script>
// DOM API를 이용하여 이메일 입력 상자를 알아낸다.
var email = document.getElementById('email');
var state = document.getElementById('state');
var btn = document.getElementById('signupBtn');

// 사용자가 버튼을 클릭하는 사건(event)이 발생했을 때
// 호출될 함수(event listener = event handler = callback)를 등록한다.
btn.addEventListener('click', function() {
  // 입력 상자에 들어있는 값을 검사하여 이메일 중복 여부에 따라
  // 아이콘을 출력한다.
  if (email.value == "hong@test.com") { // 존재하는 사용자일 경우
    //state.innerHTML = "가";
    //state.innerHTML = "\uac01"; // 이스케이프(escape) 문자를 사용하여 지정하기
    //state.innerHTML = "&#xac02;"; // HTML에 미리 정의된 상수 값(html character entity)
    //state.innerHTML = "&#44036;"; // 10진수 html character entity 값
    state.innerHTML = "\uf00d";
    state.style["color"] = "#ff0000";
  } else {
    state.innerHTML = "\uf00c"; //"&#61452;";
    state.style.color = "#0000ff";
  }
```

![7-9 네이버 예시](CSS%20%E1%84%89%E1%85%A1%E1%84%8B%E1%85%AD%E1%86%BC%E1%84%87%E1%85%A5%E1%86%B8%20(2)%20b8c6229d1e6d4a62ae6cb94b2fcaa67e/Untitled%202.png)

7-9 네이버 예시

```css
7-11 # 배경 응용 IV
    => 제목 대신에 그림을 출력할 때 배경으로 처리한다.

```
