# Bootstrap

교재: Do it! 웹표준의정석
작업중: In progress
태그: Dev, 웹&모바일, 웹프로그래밍기초
학습일: 12/21/2022

### 실습-UI 컴포넌트 다루기

CSS class 지정으로 스타일 사용 가능

`e.classList.add`

### CDN 방식으로 라이브러리 파일 지정 : 속도개선 (실무에서 x)

content delivery network : 외부 사이트에 있는 content 를 연결

![Untitled](Bootstrap%209edb8bb8dfbe4b0aafef3be272a2cf70/Untitled.png)

같은 서버에서 받은 파일은 중복으로 다운로드 하지 않는다 

→ 다운로드 시간 절약 

→ 페이지 로딩 시간 절약

<aside>
💡 문제점
의존 라이브러리가 외부에 있다 = 통제불가 = 관리 보안에 불리하다
→ 해킹 코드 삽입 방지 불가

→ 외부 서버 다운에 대비 불가

→ 따라서, 정부, 금융, 국방 등에서 CDN 방식 비선호

</aside>

### 외부라이브러리 관리

![Untitled](Bootstrap%209edb8bb8dfbe4b0aafef3be272a2cf70/Untitled%201.png)

같은 파일 중복 다운로드

→ 각 서버에서 의존 라이브러리 관리

→ 보안이 용이

<aside>
💡 문제점
네트워크 오버헤드 발생

</aside>

> 
> 
> 
> ### 외부라이브러리 다운로드
> 
> - 웹페이지 루트 폴더 (nodejs와 유사)
> 
> ![Untitled](Bootstrap%209edb8bb8dfbe4b0aafef3be272a2cf70/Untitled%202.png)
> 
> ```bash
> npm init 
> npm install jquery
> npm install jquery-ui --save
> npm install bootstrap@5.2.3 --save
> ```
>