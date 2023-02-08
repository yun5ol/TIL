# Java (25) - 통신방식 변경 (ful→less) / thread

작업중: In progress
태그: Dev, 백엔드프로그래밍, 웹&모바일, 자바프로그래밍기초
학습일: 02/03/2023

## Networking  review

### Client / Server Protocol

네트워킹은 항상 protocol 규칙 정의할 것 & 서버와 클라이언트 주고받기

> 프로토콜 규칙
> 
> - 기본 Protocol
>     - 요청
>     
>     protocol 1 : 데이터명
>     
>     protocol 2 : 액션
>     
>     protocol 3 : 파라미터 (선택사항)
>     
>     - 응답
>     
>     상태코드(문자열)
>     
>     성공 200, 서버오류 5xx, 클라이언트오류 4xx
>     
>     데이터(JSON 텍스트)
>     

### 실습

![Untitled](Java%20(25)%20-%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%89%E1%85%B5%E1%86%AB%E1%84%87%E1%85%A1%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%87%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20(ful%E2%86%92less)%20thread%207ddfea3b9b114ec3a86bcf098ae198dc/Untitled.png)

![Untitled](Java%20(25)%20-%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%89%E1%85%B5%E1%86%AB%E1%84%87%E1%85%A1%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%87%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20(ful%E2%86%92less)%20thread%207ddfea3b9b114ec3a86bcf098ae198dc/Untitled%201.png)

# server.NetworkingBoardDao
1. findAll()

try~catch 문 (서버 요청/ 응답)

```java
@Override
  public Board[] findAll() {
    try {
      // 서버에 요청
      out.writeUTF("board");
      out.writeUTF("findAll");

      // 서버의 응답
      String status = in.readUTF();
      if (status.equals("400")) {
        throw new DaoException("클라이언트 요청 오류");
      } else if (status.equals("500")) {
        throw new DaoException("서버 실행 오류");
      }// 200 이면 서버에서 보내준 보드객체를 읽어들임 'fromJson'
      return new Gson().fromJson(in.readUTF(),Board[].class);

    } catch (DaoException e) {
      throw e;
    } catch (Exception e) {
      throw new DaoException("오류 발생", e);
    } // catch 둘을 구분한 이유 : 입출력 관련 오류는 사유를 알기 위해
  }
...
```

클라이언트앱도 수정

1. serverApp 수정
    
    servlet 수정
    
    service() 
    
    ```java
    try (ServerSocket serverSocket = new ServerSocket(port);
            Socket socket = serverSocket.accept(); // 연결대기
            DataInputStream in = new DataInputStream(socket.getInputStream());
            DataOutputStream out = new DataOutputStream(socket.getOutputStream())) {
    
          StudentServlet studentServlet = new StudentServlet("학생");
          TeacherServlet teacherServlet = new TeacherServlet("강사");
          BoardServlet boardServlet = new BoardServlet();
    
          // 클라에서 보내는 데이터 1번 dataName 읽기
    			// write로 보낸거 read로 받기
          String dataName = in.readUTF();
          switch (dataName) {
            case "board":
              boardServlet.service(in, out);
              break;
          }
    ...
    ```
    
    servlet 수정
    
2. 리팩토링
    
    ### CORBA
    
    : RMI와 달리 다른 언어 간에도 통신 가능
    
    ![Untitled](Java%20(25)%20-%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%89%E1%85%B5%E1%86%AB%E1%84%87%E1%85%A1%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%87%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20(ful%E2%86%92less)%20thread%207ddfea3b9b114ec3a86bcf098ae198dc/Untitled%202.png)
    
    remote : 다른 프로세스 (실행중인 프로그램 : 공장)
    
    ⇒ 같은 컴퓨터에서 실행하는 다른 프로그램도 remote 객체이다
    
    ORB는 remote객체를 만드는 개발자가 만든다 
    
    ⇒ 이걸 대신 짜주는 기능이 위 *RPC ….→ RESTful service 
    
    # NetworkingBoardDao
    
    fetch ⇒  각 메서드의 중복 코드 삭제 가능 & fetch() 호출
    
    일관성있게 모두 데이터를 보내기로
    

```java
b.servlet

out.writeUTF("200");
out.writeUTF("success");
```

---

공통으로 쓰는 vo 분리 후 **build스크립트** 수정

![Untitled](Java%20(25)%20-%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%89%E1%85%B5%E1%86%AB%E1%84%87%E1%85%A1%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%87%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20(ful%E2%86%92less)%20thread%207ddfea3b9b114ec3a86bcf098ae198dc/Untitled%203.png)

![server도 마찬가지](Java%20(25)%20-%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%89%E1%85%B5%E1%86%AB%E1%84%87%E1%85%A1%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%87%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20(ful%E2%86%92less)%20thread%207ddfea3b9b114ec3a86bcf098ae198dc/Untitled%204.png)

server도 마찬가지

build.gradle > dependencies

```
dependencies {
    implementation project(':app-common')
```

프로젝트명은 폴더이름과 동일하게

![Untitled](Java%20(25)%20-%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%89%E1%85%B5%E1%86%AB%E1%84%87%E1%85%A1%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%87%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20(ful%E2%86%92less)%20thread%207ddfea3b9b114ec3a86bcf098ae198dc/Untitled%205.png)

Split functionality across multiple subprojects?:
1: no - only one application project
2: yes - application and library projects
Enter selection (default: no - only one application project) [1..2] 2

---

project 폴더 플러그인 복사 >common (build.gradle)  :plugins{ id ‘`java-library`’

새로 gradle & import 후 분리 완료!

각 프로퍼티>Path에서 확인 가능

---

client > Network > 해당 메서드 수정

server > service > servlet > service > 해당 메서드로

## 33-0. 전처리 & overview

- ServerApp2 백업 : 서버 종료 방지
    
    서버앱 실행되자 마자 인스턴스필드에서 객체 생성
    
    service()로 가서 바로 load받고 accept 대기 또는 processRequest(Socket socket)로 이동
    
    파라미터로 받은거 socket2에서 받기 ⇒ socket 자동 close 위해
    
    응답 오면 processRequest로 넘어옴
    

- Networking 연결방식 2 가지
    - Connection Oriented (연결지향) : TCP / eg.전화, LOL, 구글미트 …
        
        ㄴStateful : 통신이 여러번 & 먼저 접속한 클라이언트가 연결을 끊을 때 까지 진행됨 / eg. 상담전화
        
        한 클라이언트가 오랜 시간 연결되어 있으면 다른 클라이언트의 대기 시간이 길어진다.
        
        > 프로토콜 : SSH, TElnet, FTP, 채팅
        > 
        
        ㄴStateless :  통신 1번씩 & 서버의 응답을 받으면 자동으로 연결을 끊는다 / eg. 114안내
        
        한번 연결에 한번 요청/응답이므로 다른 클라이언트의 대기 시간이 적다.
        
        ⇒ 더 많은 클라이언트의 요청을 처리할 수 있다.
        
        > 프로토콜 : HTTP1/2
        > 
        
        - 연결하는 과정에서 시간을 소요 (3 Way Handshake)
        - 다만, 연결 후에 데이터를 전송하기 때문에 신뢰성을 보장한다
    
    - Connectionless (비연결성) : UDP / eg. 방송,  택배, 편지, ping
    
    - 연결 과정이 없어서 시간을 절약
    - 다만, 연결 확인 없이 데이트를 전송하기 때문에 신뢰성이 떨어진다

<aside>
📍 HTTP1/2 → 3 으로 바뀌면서

TCP → UDP  로 바뀜 (시간 절약)

</aside>

## 33.  통신 방식을 Stateful → Stateless 로 변경

- 현재의 TCP를 UDP로
1.  서버앱 while문만 제거하면 완료
2. 클라앱
    
    quit 삭제
    
    execute에서 만들던 socket 을 fetch로
    
3. 네트워크보드디에이오
    1. fetch 연결될 때 소켓 연결로 변경
        
        요청할 때마다 연결한다
        
4. common
    1. daostub 으로 fetch() 빼기
    2. daoException 또한
    
    <aside>
    📍 DaoStub class 만든 이유
    stateful → stateless 로 각 dao마다 fetch() 에 적용 후,
    코드 중복 & 클라이언트 브로커 역할을 위해 stub으로 따로 뺌
    ⇒ dao를 직접 이용하지 않아도 된다
    
    </aside>
    

## 34. Thread로 멀티태스킹 구현  : 동시요청 처리

- 위 방식의 단점
    - 앞서 통신 시간이 길게 소요되면, 대기시간이 길어지는건 마찬가지다

- 현 상황 : 멀티스레드 적용 전
    - main Thread 하나로만 순차 처리

- 멀티 스레드 적용
    - 각 클라이언트 마다 서브 스레드를 생성
    - 메인 스레드의 역할은 “접수”
        
         & 서브 스레드가 실제 요청을 처리
        
    

결론, 여러 스레드를 동원하여 여러 클라이언트 요청을 동시처리

(쓰레드 전 serverApp3 로 백업)

### Thread 작동 방법

실무에서 굉장히 다양하다

- 상속
- 서브클래스 생성
- 익명클래스로 서브클래스 생성
    - run() Override{}.start();
    
    ```java
    Socket socket = serverSocket.accept();
            new Thread() {
              @Override
              public void run() {
                processRequest(socket);
              };
            }.start();
    ```
    
- 인터페이스 구현
    1. requestprocessor class 생성
    2. 익명클래스로 러너블 구현체.start
    3. **new** Thread( **new** RequestProcessor(socket)).start();
    
    cf. 람다
    

---

## multi-tasking

- single-tasking
    
    eg. DOS
    
    - 순차적 실행으로 cpu를 100% 활용할 수 없다.

- multi-tasking
    
    eg. Windows
    
    - 시간을 쪼개서 여러 app을 돌아다니면서 명령어를 실행 ⇒ 사분할 시스템
    - 여러 App이 동시에 실행되는 것 처럼 보이나, 그렇지 않다. ⇒ 시간을 쪼갠 것이다.

### 멀티태스킹 기법 : 다중 클라이언트 요청 처리

1. 프로세스 복제 ‘fork()’
    - 요청이 들어오면 서버를 복제하여 요청/응답 처리
    - 서버를 복제할 때 서버가 사용하는 메모리는 2종 (heap, Stack) 또한 함께 복제된다
    - 따라서, 부모프로세서와 자식프로세서라 칭한다
        
        <aside>
        📍 문제점
        1.  프로세스 (서버 프로그램)가 사용하는 메모리도 그대로 복제된다.
            ⇒ 메모리 낭비가 심하다
        2.  자식프로세스는 부모프로세스를 종료하더라도 종료되지 않는다.
            ⇒ 복제한 자식 프로세스 제어가 힘들다.
        
        </aside>
        
2. 멀티스레드
    - 요청이 들어오면, 서버는 스레드를 생성하여 요청/응답 처리
    - 여기서 메모리는 stack만 생성하며,  heap메모리는 프로세스 것으로 공유한다.
    - 요약
        - 프로세스 heap메모리 공유 ⇒ 객체 중복생성이 적다 ⇒ 메모리 낭비가 적다
        - 프로세스 종료되면 스레드도 종료된다 ⇒ 스레드가 프로세스에 종속된다

### JVM과 스레드

+))) 그림추가할 것

JVM에서 main()으로 이어지는 작업 흐름이 한 줄로 이어진 실타래와 같다 ⇒ “Thread”라 부른다

JVM이 여러개의 버츄얼 머신을 실행시키고, main 메서드를 실행시키는 건 main 메써드다

**package** com.eomcs.concurrent.ex2

- 스레드 자체는 운영체제가 만들고 운영체제 것이다. (CPU 스케쥴링에 따라)
    
    그래서 맥과 윈도우 별로 조금씩 다를 수 있다.
    
    따라서 JVM이 스레드를 완전 조정할 수 없다
    
    → 최신 해결책 openjdk19! 가상쓰레드
    
    추상화 계층을 생성하여, JVM이 가상쓰레드로 스케쥴링하며, JVM은 운영체제와 프로그램 사이를 중재한다
    

### 부모스레드와 자식스레드

![Untitled](Java%20(25)%20-%20%E1%84%90%E1%85%A9%E1%86%BC%E1%84%89%E1%85%B5%E1%86%AB%E1%84%87%E1%85%A1%E1%86%BC%E1%84%89%E1%85%B5%E1%86%A8%20%E1%84%87%E1%85%A7%E1%86%AB%E1%84%80%E1%85%A7%E1%86%BC%20(ful%E2%86%92less)%20thread%207ddfea3b9b114ec3a86bcf098ae198dc/Untitled%206.png)

### CPU 스케쥴링

: 프로세스에게 CPU를 배정하는 것

- 운영체제는 프로세스의 명령을 실행하는 순서나 시간을 제어한다
    
    그 방식은
    
    1. Round-Robin (Window OS)
        
        모든 프로세스를 동일한 실행 시간으로 제어한다
        
        우선순위가 실행에 영향을 덜 끼친다
        
    2. Priority + Aging 기법 (Linux/Unix) : 우리가 쓰는!
        
        우선순위가 높은 프로세스에게 실행 횟수나 시간을 더 부여한다
        
        우선순위가 실행에 영향을 끼친다
        

### ㄴCPU 스케쥴링과 스레드

- OS는 스레드에 대해서도 프로세스와 동일한 자격으로 스케쥴링한다.
    - 프로세스가 받은 시간을 쪼개서 스레드가 나눠 사용하는 것이 아니다.

### ㄴCPU 스케쥴링과 Context Switching

: 실행 정보와 명령을 cpu 캐시 메모리에 적재하는 것

- CPU 스케쥴링 정책에 따라 프로세스를 돌아가면서 실행할 때,  
     이전 프로세스의 실행 정보를 보관하고,
     다음 프로세스의 실행정보를 적재한다
    - OS가 프로세스를 실행하면, 캐시메모리를 CPU의 L1에 적재한다
    - 다른 프로세스 또한 적재하며, 기존 프로세스의 실행정보는 캐시메모리에 보관한다
- 이때, 너무 짧은 시간 동안 너무 자주 프로세스를 교체하면, 
명령을 실행하는 시간보다 Context Switching 시간이 더 많이 소요되기 때문에 비효율적이다
    - 따라서, 적절한 시간에 따라 프로세스를 교체해야 한다

### Critical Region = Critical Section

: 여러 스레드가 동시에 실행할 때 문제가 발생할 수 있는 코드 영역

⇒ 동기화(Synchronize)를 이용해서 제어한다

ex. 누가 화장실에서 볼일 보는데 그 사람 위에서 볼일 볼 수 있냐고!

ex. 예매 시스템

- `Semaphore`(1) ~ Semaphore(5)… 이런 식
    
    “동시진입 제어” 따라서, Semaphore는 Mutex 이다!
    
    > Mutex (오직 한개만)
    > 
    > 
    > ex. 선풍기 버튼 : 4개의 버튼이 있어도 하나의 스위치만 선택 가능 & TV채널 & 라디오 …
    > 
    > ⇒ “상호배제 Mutual Exclusion” 
    > 

한 번에 한 스레드 만이 호출하도록 접근을 제한하고 싶다면

메서드 전체를 동기화 블록으로 선언하라!

어떻게?

메서드 앞에 synchronized를 붙인다.

=> 여러 스레드가 동시에 접근했을 때 문제가 발생하지 않는 코드에 대해

**synchronized** 사용한다면 실행 속도가 떨어질 것이다.

=> 왜?

한 번에 한 스레드만 순차적으로 접근하기 때문이다.

이렇게 크리티컬 섹션에 동시에 접근하지 못하게 하는 기법

=> "뮤텍스(mutex)" 또는 "세마포어(1)(semaphore)"라 부른다.

자바에서 뮤텍스를 구현하는 방법,

=> 크리티컬 섹션에 해당하는 메서드나 코드 블록에

**`synchronized`** 키워드를 붙여

한 번에 한 스레드만 진입할 수 있도록 lock을 건다.

참고!

=> 여러 스레드가 동시에 실행해도 문제가 없는 코드 블록을

"스레드 안전(thread safe)"라 부른다.

**package** com.eomcs.concurrent;