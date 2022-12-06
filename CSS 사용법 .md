# 🖌 CSS 사용법

📓 교재: Do it! 웹표준의정석  
✔ 작업중: In progress  
🏷 태그: Dev, 웹&모바일, 웹프로그래밍기초  
📆 학습일: 11/28/2022  

# 목차
1. CSS

## 1. CSS

Cascading Style Sheet : HTML element 의 모양을 정의한다.  
부모태그의 스타일이 자식태그에 상속되거나, 중첩되기도 하며,  
상속되는 태그가 있는 것도, 아닌 것도 있다.  

![image](https://user-images.githubusercontent.com/118426836/204231887-6688f749-8987-4957-8cb0-8abbc063e2f1.png)


**< CSS 의 핵심 >**

- selector 사용법 !!
    - 셀렉터 { 스타일:값; 스타일:값;… }
    - 동일한 스타일을 넣으려니 반복이 귀찮아서 SASS 라는 변형을 사용하기도
- specificity : 스타일 적용 순서 !!
- box 다루는 방법 : 테두리, 여백, 박스 계산법
- 폰트 다루는 방법
- 색상 지정 방법
- 배경 다루는 방법
- 블록과 인라인 다루는 방법
- 위치 조정하는 방법

….. 그 이상은 CSS 고급에서 다룰 것

### 1.1 Selector

- 셀렉터 { 스타일:값; 스타일:값;… }
- 동일한 스타일을 넣으려니 반복이 귀찮아서 SASS 라는 변형을 사용하기도

| 종류 | 예시  |
| --- | --- |
| * { } |  |
| 태그명 { } | body { } |
| 태그명, 태그명, 태그명 { }  | img, ul { } |
| .그룹명 { }  | .c1, .c2 { } |
| #태그아이디 { } |  #content { } |
| -[속성명:값] { } |  |
| -:상태명 { }    pseudo selector |  li:hover { } |

![image](https://user-images.githubusercontent.com/118426836/204231991-470640dd-149f-443a-bfe8-056477601806.png)


![image](https://user-images.githubusercontent.com/118426836/204230733-c3c11732-4302-4228-9fa2-494d396534af.png)


![image](https://user-images.githubusercontent.com/118426836/204232042-95b33017-140e-47a0-a5e9-da95d7777eda.png)

- 부모 태그와 자식 태그의 계층 구조 : UI는 아래와 같이 차곡차곡 계층화됨

![image](https://user-images.githubusercontent.com/118426836/204230811-e10e5780-d97b-4f81-aec5-b1b448e6c243.png)

> body에 배경을 그레이로 설정
> 
> 
> p까지 배경 색상이 상속 될 텐데, p에 다시 한번 배경색 설정?
> 
> 이렇게 쓸데 없는 출력을 줄이는게 중요! 프론트앤드의 기술이다. =Virtual DOM????
> 

  
![image](https://user-images.githubusercontent.com/118426836/204232214-325e2979-a24a-4cdf-a66f-812a9dba991b.png)


![image](https://user-images.githubusercontent.com/118426836/204230895-55fbb0ac-1cb3-4efb-a500-cae1e3e505ce.png)
> li태그는 블록태그 : 한라인 독점  

![image](https://user-images.githubusercontent.com/118426836/204232376-fb7b4430-efdd-4886-8a6d-17f08af81337.png)


![image](https://user-images.githubusercontent.com/118426836/204231086-e1223ffa-af35-464f-8d01-d664815ed521.png)


![image](https://user-images.githubusercontent.com/118426836/204232469-2946fa07-aa1d-46de-a0ec-4dc5515059c0.png)

![image](https://user-images.githubusercontent.com/118426836/204231180-30447649-46f5-42dc-acb4-502880577d9f.png)
> ‘다음 태그’의 개념! ‘형제’, 자손x  


![image](https://user-images.githubusercontent.com/118426836/204232794-fdbf9b86-0461-4ca2-9a50-c9fdeae95e12.png)
![image](https://user-images.githubusercontent.com/118426836/204232846-14c813e4-0079-477d-8c4a-fbb3bb7cbf0e.png)
![image](https://user-images.githubusercontent.com/118426836/204232905-42ded649-9d45-4919-b52a-91834daf28ee.png)


### 1.2 checkbox, radio, select
![image](https://user-images.githubusercontent.com/118426836/204233032-0d9c4c87-79b2-4d7c-8243-5e3997b918a4.png)
![image](https://user-images.githubusercontent.com/118426836/204233099-d789eed3-7f9e-4622-9fcc-6f8c08b3d9e8.png)


