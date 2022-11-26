# 🐱‍👤 HTTP 프로토콜

📗 교재: Do it! 웹표준의정석  
✔ 작업중: In progress  
🏷 태그: Dev, 웹&모바일, 웹프로그래밍기초  
📆 학습일: 11/25/2022  

## 1. 요청과 응답 규칙

### 1.1 네트워킹

- Connectionless (비연결) : 연결 없이 데이터 전송 eg. 편지, 방송
    - **UDP** : 데이터 전송 신뢰성 없으므로 별도의 처리 필요 (HTTP 3)
- Connection-oritented (연결 지향) : 연결 후 통신 eg. 전화
    - **TCP** : 데이터 전송 신뢰성 확보 (HTTP 1, 2)
    
    > Connetion-oritented
    > 
    > - stateful : 적은 수의 클라이언트에 대응
    >     
    >     1번의 연결 후 연결이 끊길 때 까지 연결-요청-응답 과정을 반복 (1회 연결, 다회 통신)
    >     
    >     “thread 기술”
    >     
    > - stateless : 많은 수의 클라이언트에 대응 가능
    >     
    >     1번의 연결 후 연결-요청-응답 과정을 거치고 연결을 끊음 (1회 연결, 1회 통신)
    >     
    >     **HTTP는 stateless**, 즉 state 를 저장하지 않는다. 요청/응답하는 정보가 저장되지 않는다.
    >     

![image](https://user-images.githubusercontent.com/118426836/204090401-9ed00717-2629-481a-ba42-c061a9217c86.png)


### 1.2 proxy server

: client 와 server 사이 통신을 중재

![image](https://user-images.githubusercontent.com/118426836/204090414-b8d82639-ecc4-4ba8-bc93-4cfe6d4f5679.png)


클라이언트가 프록시서버에 요청

➡프록시서버가 서버에 요청

➡서버가 프록시서버에 응답

- cache 가 프록시서버로 부터 응답 데이터를 보관
    
    →같은 자원을 요청할 때 보관된 데이터를 즉시 전달
    
    →네트워크 오버헤드 감시
    
    →응답 속도 개선
    
- cache가 프록시서버를 모니터링 (HTTP 통신을 살펴볼 수 있음)
    
    →요청/응답 내용 감시
    
    →보안 강화
    

➡프록시 서버가 클라이언트에 응답

### 1.3 request 규칙

- **starter line**

해당 request가 어떤 action을 의미하는지 정보를 담는다. request target (URL) 어떤 곳에다가 요청하는지 내포한다.

- **header**

해당 request에 대한 추가 정보를 담고있다.

key : value 값

request target 도 주소. host도 주소. 두 개를 합쳐서 보고 서버가 알게 된다.

- **body**

데이터가 담겨있는 부분.


![image](https://user-images.githubusercontent.com/118426836/204090470-b1b4b02f-4b09-4b81-bbd8-f9d181979849.png)



### 1.4 response 규칙

- **status line**

response의 상태를 간략하게 나타내는 부분으로 3가지로 구성

HTTP버전

status code : 응답 상태를 나타내는 코드

status text : 응답 상태를 간략하게 설명해주는 부분

- **headers**

응답에 대한 부연 설명

다만 response에서만 사용되는 header 값들이 있다. eg. `User-Agent` 대신 `Server` 헤더가 있다.

- **body**

response의 body와 일반적으로 동일하다.

request와 마찬가지로 모든 response가 body 가 있지는 않다. 데이터를 전송할 필요가 없을 경우 body는 비어있다.

![image](https://user-images.githubusercontent.com/118426836/204090503-81180518-2be4-496c-9799-01f58e143975.png)


### 1.5 HTTP method 란?

: http request 가 의도하는 action을 정의한 것.

`get`

서버로 부터 데이터를 취득

`post`

서버에 데이터를 추가, 작성 등, 이때 보내는 데이터는 message-body

`put`

데이터를 갱신, 작성 등 

`delete`

데이터를 서버에서 삭제요청

> **CRUD**
> 
> 
> Create, Read, Update, Delete 를 의미
> 
> HTTP 메소드에서 get, post, put, delete 가 각 CRUD 역할을 한다.
> 
> - Create : post/put
> - Read : get
> - Update : put
> - Delete : delete

## 2. get/post요청 비교 :get 요청

**get request** : 서버로 부터 정보를 가져오는 method

단순히 서버에서 가져오는 것이라, 브라우저에 캐쉬도 되고 아래 처럼 URL에 query string이 그대로 노출된다.

![image](https://user-images.githubusercontent.com/118426836/204090517-83d9c3e5-5305-4046-acee-f17d42f58110.png)


❗ **한계** 

- 바이너리 데이터를 보낼 수 없다 : 포맷이 깨진다.
    - 바이너리 데이터를 텍스트로 인코딩하면 가능
- URI 크기의 제한 때문에 대용량 데이터를 보낼 수 없다.
- URL > 브라우저 캐시에 보관 : 보안이 안 된다.
- content-type이 없다.

> **text 데이터** : 일반 텍스트 편집기로 편집 가능한 포맷
> 
> 
> eg. .txt, .rtf, .html, .css, .js, .xml, .json, .properties, .java, .py …
> 
> **binary 데이터** : byte 단위로 포맷, 일반 텍스트로 편집 불가하며 전용 app. 사용 (포맷이 깨진다)
> 
> eg. .jpeg, .gif, .png, .mp3, .mp4, .avi, .doc …
> 

## 3. get/post요청 비교 :post 요청

**post request** : 서버에 정보를 추가하거나 변형하는 method

URL에 요청하지 않고 별도의 payload (전송되는 data) 에 정보를 담아 요청한다.

- binay 데이터 전송 가능
- URL에 노출되지 않음
- 여러개의 파일 첨부 가능
- 용량 제한 x
- content-type이 있다.

> **multipart/form  data 형식으로 파일을 업로드 하는 방법**
>name 옵션이 없는 데이터 값은 서버에 전송하지 않는다.
> 
> 기본 인코딩 폼 
> application/x-www-form-urlencoded enctpy=”multipart/form-data”
> ➡인코딩 폼을 변경
> ➡파일 자체 서버에 전송
> 
> 타입 file 에 multipart 를 붙여야 여러개의 파일 전송이 가능하다.
