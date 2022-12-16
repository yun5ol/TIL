# AJAX

교재: Do it! 웹표준의정석
작업중: In progress
태그: Dev, 웹&모바일, 웹프로그래밍기초
학습일: 12/16/2022

## AJAX

### Asynchronous JavaScript XML (비동기)

현재 어플리케이션의 실행을 유지한 상태에서 서버에 자원을 요청하는 기술

[https://expressjs.com/ko/starter/installing.html](https://expressjs.com/ko/starter/installing.html)

`$ npm install express --save`

---

`$ npm install`

1. 명령을 실행하는 작업 폴더에서 package.json 파일을 찾는다.
2. package.json 파일에 등록된 라이브러리들을 다운로드한다.
    1. node_modules 폴더가 없으면 생성한다.
    2. 라이브러리가 없으면 다운로드 한다.
        1. 설정된 조건에 따라 버전을 검사해서 적절한 버전을 다운로드 한다.

---

`$ npm install 라이브러리명`

1. 해당 이름을 가진 라이브러리를 다운로드한다.
    1. node_modules 폴더가 없으면 생성한다.
    2. 라이브러리가 없으면 다운로드 한다.
        1. 설정된 조건에 따라 버전을 검사해서 적절한 버전을 다운로드 한다.

### npm 사용법

1. `npm init` → package.json 생성
2. `npm install 라이브러리 - -save` → 라이브러리 다운로드
3. `npm install` → Git Repo. 에서 프로젝트를 가져온 후 1회 실행

12/16~

> UI Component
> 
> 
> 
> nodejs는 모두 서버에서 쓰는 명령어 (백엔드)
> 
> **JSON.stringify** serialization (직렬화) : 객체를 JSON 문자열 형태로 바꾸는 것
> 
> = encoding 
> 
> ↔ **JSON.parse** deserialization (역직렬화) = decoding
> 
> ![객체 <==========================>문자/바이트
> 데이터 덩어리           일련의(serial) 연속적인 알갱이들의 배열](AJAX%20af08c3bdf5ee4e49bd479dfbbfc94bdc/Untitled.png)
> 
> 객체 <==========================>문자/바이트
> 데이터 덩어리           일련의(serial) 연속적인 알갱이들의 배열
> 
> querystring (?) : 사용자가 입력 데이터를 전달하는 방법중의 하나로, url 주소에 미리 협의된 데이터를 파라미터를 통해 넘기는 것을 말한다.
> 
> ```jsx
> xhr.open("GET", "http://localhost:3000/proxy?url=" + url.value, false); // ? 느낌표로 구분하며 뒤부터가 쿼리스트링 
> //GET 요청으로 보내는 payload (데이터)
> ```
> 
> route parameter
> 
> ### Route parameters
> 
> - ex) GET /artists/1, GET /artists/1/company/entertainment
> 
> ```jsx
> const express = require('express');
> const router = express.Router();
> 
> router.get('/artists/:id', function (req, res) {
>   console.log("id는 " + req.params.id + " 입니다")
>   res.send("id : " + req.params.id)
> });
> 
> // 여러개도 가능
> router.get('/artists/:id/company/:company', function (req, res) {
>   res.send("id : " + req.params.id + " 회사 : " + req.params.company)
> });
> ```
> 
> ### Query string
> 
> - ex) GET /artists?name=hello
> 
> ```jsx
> const express = require('express');
> const router = express.Router();
> 
> router.get('/artists', function (req, res) {
>   console.log("이름은 " + req.query.name + " 입니다")
>   res.send("name : " + req.query.name)
> });
> ```
> 

### CORS (cross origin resource sharing)를 우회하는 방법

ex07 > 02-1 / [https://security-log.tistory.com/20](https://security-log.tistory.com/20)

: origin 을 건너서 자원 공유

CORS 정책 : HTML 을 다운로드 받은 원래 (origin) 서버로만 AJAX 요청 가능 (웹크롤링 방지)

> <**해결방안> # ex07 > 1-4**
> 

**요청 대행 proxy 서브를 활용한다. (실무 방식)**

: origin 서버는 웹 브라우저가 아니기 때문에, CORS 정책과 무관하다.

![origin server : **proxy** 역할](AJAX%20af08c3bdf5ee4e49bd479dfbbfc94bdc/Untitled%201.png)

origin server : **proxy** 역할

> **AJAX 요청과 일반 요청의 차이**
> 
> 
> 일반요청 : 화면을 변경
> 
> AJAX 요청 : 현재 화면 유지한 채 서버 요청
> 
> eg. naver 첫페이지 날씨 슬라이딩
> 

### GET 요청

```jsx
// http 요청을 다루는 라이브러리 로딩하기
const request = require('request');
...
// 클라이언트 요청을 다른 서버에게 보낸다. 
// 프록시 생성코드
app.get('/exam01-1', (req, res) => {      

  res.set('Access-Control-Allow-Origin', '*'); // CORS 문제 해결
  res.set('Content-Type', 'text/plain; charset=UTF-8'); 

  request.get({
    uri: req.query.url // options, function
  }, (error, response, body) => {
    res.send(body);
  });
});
```

```jsx
<body>
<h1>AJAX - GET 요청</h1>

<h2>일반 GET 요청</h2>
<form action="http://127.0.0.1:3000/exam02-1" method="get">
이름: <input type="text" name="name"><br>
나이: <input type="text" name="age"><br>
<button type="submit">등록</button> 
<button type="reset">초기화</button>
</form>

<hr>

<h2>AJAX GET 요청</h2>
<button id="btn1">요청</button><br>
<textarea id="ta" cols="80" rows="10"></textarea>

<script>
"use strict"

const ta = document.querySelector("#ta");

document.querySelector("#btn1").onclick = () => {
    var xhr = new XMLHttpRequest();
    
    // GET 요청은 데이터를 URL에 붙인다. 
    xhr.open("GET", "http://127.0.0.1:3000/exam02-1?name=홍길동&age=20", false);
    xhr.send();
    ta.value = xhr.responseText;
};

</script>
</body>
```

### AJAX POST 요청

![Untitled](AJAX%20af08c3bdf5ee4e49bd479dfbbfc94bdc/Untitled%202.png)

```jsx
app.post('/exam02-2', (req, res) => {        // 프론트앤드     
  res.set('Access-Control-Allow-Origin', '*'); 
  res.set('Content-Type', 'text/plain; charset=UTF-8'); 

var payload = `이름: ${req.query.name}\n`; // \n : 줄바꿈 코드
  payload += `나이: ${req.query.age}\n`;

  res.send(payload);
});
```

```jsx
<form action="http://127.0.0.1:3000/exam02-2" method="post"> // 생략시 get 요청
...
xhr.setRequestHeader(
        "Content-Type", 
        "application/x-www-form-urlencoded");

```

### 동기요청의 한계

서버에서 응답을 할 때까지 send() 메서드는 리턴하지 않는다.
따라서 작업 시간이 오래 걸리는 경우 send() 메서드가 리턴하지 않아서  
다른 작업을 수행하지 못하는 상황이 발생한다.

**onreadystatechange  (**이벤트 핸들러)

**readyState**

### **AJAX - 응용 I : HTML 일부분 가져오기**

> **AJAX 의 응답결과가 JSON 또는 XML 데이터인 이유?**
> 
> 
>  멀티 디바이스에 대응할 수 있다.
> 
> ![Untitled](AJAX%20af08c3bdf5ee4e49bd479dfbbfc94bdc/Untitled%203.png)
> 

npm app.js 

localhost;3000/exam06-1