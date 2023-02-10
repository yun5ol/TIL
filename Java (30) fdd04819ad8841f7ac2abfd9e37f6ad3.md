# Java (30)

작업중: In progress
태그: Dev, 백엔드프로그래밍, 웹&모바일, 자바프로그래밍기초
학습일: 02/10/2023

## 36. DB 커넥션 공유

1. 이전

SQL 실행할 때마다 (DAO의 메서드를 호출할 때 마다) DBMS에 연결/끊기 반복

⇒ 연결될 때 마다 사용자 인증(Authentication)을 수행 + 권한(Authorization)을 부여 

: `“Auth”`

인증(Authentication : 사용자 유효 여부 검사) 

ID/PW일치여부

권한(Authorization : 사용자의 권한 검사

database 접근 가능?

SQL 명령 사용 범위

- 문제점
    
    매번 연결 때 마다 시간이 소요된다
    
1. 해결책
    
    각  App. 별로 DB Connection (& Tread) 를 분리/ 공유한다
    

> **시스템 간 데이터 공유 사례**
> 
> 
> 
> eg. 회계시스템 → 인사시스템
> 
> 회계팀은 인사팀 DBMS에 접근할 수 없다
> 
> - vendor가 다르거나 플랫폼(C# 또는 Java 등)이 다른 경우, DB접근이 차단된다
>     
>     
>     ⇒ 정보 요청(REST API)시,  JSON이나 XML형태로 데이터를 주고 받는다.
>     
>     위 과정을 System Integration (SI)
>     
>     <aside>
>     📍 용어정리
>     SI (System Integration) : 기존 시스템과 연계
>     SM (System Maintanence) : 기존 시스템에 새 기능 추가
>     
>     </aside>
>     
> 
> ⇒ 또는 DBMS에 guest ID를 부여, select 권한만 주어진다
> 

## 37. 어플리케이션 서버 아키텍처

1. 기존

기능이 추가/변경/삭제 될 경우, 각 PC별로 App.을 재설치해야 한다.

⇒ 유지보수가 불편

1. App을 서버에서 실행

각 PC별로 클라이언트를 설치한다.

⇒ 기능의 추가/변경/삭제 시 서버에만 수정하면 된다.

- Client 역할
    - 사용자 입력을 받아 서버에 전달
    - 서버의 응답을 출력 (특별한 기능이 없다)
- Server 역할
    - 기능 실행
    - UI 생성
    

<aside>
📍 이러한 변화는 global business (세계화) 가속로 인한 잦은 업무 변경 때문
⇒ 시대적 상황과 맞물려 PC 에서 서버로 이동하는 추

</aside>