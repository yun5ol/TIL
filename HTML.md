# 💻 HTML

📓 교재: Do it! 웹표준의정석  
✔ 작업중: In progress  
🏷 태그: Dev, 웹&모바일, 웹프로그래밍기초  
📆 학습일: 11/23/2022  


## 목차
1. HTML, HTTP
2. HTML 기본 구조  
3. 번외  


## 1. HTML, HTTP


### 1.1 HTML, HTTP 등장 전

- 프로토콜 : 통신 규칙 > 데이터 송수신  file transfer protocol
- FTP client : 카카오톡 프로그램
- FTP : 서로 파일을 주고 받을 때의 프로토콜

(그림 추가 할 것)

단점 

1. 논문이 참조하는 다른 논문을 다운로드 받기 번거롭다.
2. 논문 안에 다른 논문이 업로드 된 서버 주소가 없다. 

⬇  (요약 : 논문을 원활히 주고받으려고 http 탄생 / 이 http 제어를 html)

### 1.2 HTML, HTTP 등장 후

위 단점 보안을 위해 **다른 논문의 위치정보를 삽입 + 텍스트의 포맷을 지정** 

**(+ 추후에는 그림, 음성, 동영상 삽입 +… )**

⬇ 보안으 위해 필요한

- “**Hyper Text** (고도화된 텍스트)”
    
    고도화를 위해 별도의 표시 (형식) 이 필요 = **Markup** > **L**anguage 필요
    
    **고도화된 마크업 언어 : HTML 의 탄생**
    
    > **“Markup”**
    > 
    > 
    > 데이터를 설명하는 데이터, 데이터를 제어하는 데이터 = 부가데이터 = meta data 
    > 
    > 
- **HTTP** : Hyer-Text Transfer Protocol
    
    HTML 문서를 원활하게 받고다른 HTML 문서를 찾아가기 쉽도록 만든 통신 프로토콜
    

### 1.3 HTTP client / server App.

송수신 순서는 1. 클라이언트의 요청 2. 서버의 응답

- HTTP server (web server) : Apache HTTP server, NginX
    
    > web : HTML 문서들의 연결된 모습이 거미줄과 같다
    > 
- HTTP client (web browser) : Chrome, Safari, Firefox, Edge ``` curl, wget
    
    단순히 HTML을 다운받는 것만이 아니라 HTML을 출력하고 제어하는 역할도 한다.
    
- HTTPS : HTTP + security 암호화

### 1.4 web 기술의 활용

- [웹기술의 등장](https://www.notion.so/e6172fe100a24c7082c0ee3b63b6fc53)
- 웹기술 활용의 변화
    
   ![이미지](https://user-images.githubusercontent.com/118426836/203512492-2b84aa93-7912-4d63-acb2-fc98d3a0d2b3.png)

### 1.5 Web Application 제작 기술

**화면 만드는 기술 “프론트엔드 개발”** 

![555화면 캡처 2022-11-23 183444](https://user-images.githubusercontent.com/118426836/203513456-9150abf4-9875-453f-82e4-488b11fdcc46.png)

 

## 2. HTML 기본 구조

![image](https://user-images.githubusercontent.com/118426836/203512931-cd42e2cb-1ac1-4b14-8b02-33e1469b4fd5.png)



### 2.1 HTML 공부법

**예제를 실행해서 결과화면을 확인 > 다시 예제로 돌아가 태그의 기능을 이해하세요**

이러한 경험 후, HTML 태그 중에 그런 기능의 태그가 있다는걸 안다! 기억이 안나면 구글링!


![44화면 캡처 2022-11-23 183616](https://user-images.githubusercontent.com/118426836/203513691-a520caaa-5337-45af-86f0-1bf91aeb101d.png)

- **HTML4 doctype**

[https://www.w3.org/TR/html4/sgml/dtd.html](https://www.w3.org/TR/html4/sgml/dtd.html)
![image](https://user-images.githubusercontent.com/118426836/203513089-83d63a52-17c1-4855-80af-925d4523173a.png)



> DTD : old
> 
> 
> Schema : new
> 
> 문서규칙 : 태그를 사용하는 방법. 어떤 태그는 어떠한 경우에 사용하라!
> 

  
    
      
        
	
## 번외) 금일 실습 전 환경 설정


### git clone URL_[] : 별칭 붙여서 클론 가능

```bash
C:\Users\bitcamp\git>git clone https://github.com/eomjinyoung/bitcamp-study bitcamp-ncp-teacher
Cloning into 'bitcamp-ncp-teacher'...
remote: Enumerating objects: 68, done.
remote: Counting objects: 100% (5/5), done.
remote: Compressing objects: 100% (5/5), done.
Receiving objects: 100% (68/68), 27.90 MiB | 11.20 MiB/s, done.

Resolving deltas: 100% (21/21), done.
```

![Untitled](HTML%20e77d99514ac84dcfa4f742939dd8e52b/Untitled.png)
