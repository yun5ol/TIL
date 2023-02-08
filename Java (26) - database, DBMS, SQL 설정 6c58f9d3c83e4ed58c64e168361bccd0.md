# Java (26) - database, DBMS, SQL 설정

작업중: In progress
태그: Dev, 백엔드프로그래밍, 웹&모바일, 자바프로그래밍기초
학습일: 02/06/2023

## 35. DBMS 도입

추후 진행

### DBMS 도입 후 System Architecture

---

## DataBase

### DataBase, DBMS, SQL

DataBase

통합 관리되는 데이터 집합체

- 자료를 구조화 ⇒ 중복 제거
- DBMS에 의해 제어된다

특징

- 사용자 질의에 즉각적인 응답
- 생성, 수정, 삭제를 통하여 최신 데이터 유지
- 여러 사용자가 동시 공유
- 사용자가 원하는 데이터를 주소가 아닌, 내용에 따라 참조 가능
- 어플리케이션과 데이터베이스는 독립적으로 동작

DBMS

데이터베이스를 관리하는 응용프로그램 DataBase Management System

- 정의 : 데이터의 형식, 구조, 제약조건 등 정의
- 구축 : 데이터를 파일에 쓰고/읽기
- 조작 : 데이터 추가, 변경, 삭제, 조회
- 공유 : 동시 접근 가능
- 보호 : 접근 제어
- 유지보수 : 업데이트 가능

SQL

DBMS에 작업 요청 시 사용하는 (데이터베이스에 정보를  저장, 처리, 요청) 프로그래밍 언어 = 명령문법

크게 두 가지로 나뉨

1. DDL (Data Definition Language)
    
    테이블, 뷰, 프로시저, 함수, 트리거 등 DB 객체를 정의하고, 변경, 삭제
    
2. DML (Data Manipulation Language)
    
    테이블의 데이터를 입력, 변경, 삭제 등 데이터 조작
    
    2.2 DQL (Data Query Language) 
    
    테이블의 데이터를 조회
    
    주로  DQL도 포함하여 DML이라 부른다.
    

실무 SQL

= SQL 표준 문법 + 회사 고유 문법

⇒ DBMS 마다 SQL 문이 약간씩 다르다

⇒ App 작성 할 때 DBMS에 맞춰 SQL을 작성해야 한다

> ❗ DBMS 사용하는 이유
> 
> 
> 
> - 직접 파일 I/O 프로그래밍 할 필요가 없다
> - 데이터를 체계적으로 관리 가능하다
> - 프로그래밍 언어&도구에 상관없이, 일관되게 유지보수가 가능하다

### DBMS 학습

![Untitled](Java%20(26)%20-%20database,%20DBMS,%20SQL%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%206c58f9d3c83e4ed58c64e168361bccd0/Untitled.png)

지금까지, Myapp (어플리케이션)에서 직접 파일들을 다루었다면 이제부터 DBMS를 이용한다

how?

1. SQL로 요청/응답 처리
2. DBMS API 사용

> 
> 
> 
> ### DBMS 설치 및 설정
> 
> 아래 설치 방법 참조
> 
> ![Untitled](Java%20(26)%20-%20database,%20DBMS,%20SQL%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%206c58f9d3c83e4ed58c64e168361bccd0/Untitled%201.png)
> 
> 1. MariaDB 다운로드
> 
> [Download MariaDB Server - MariaDB.org](https://mariadb.org/download/?t=mariadb&p=mariadb&r=11.0.0&os=windows&cpu=x86_64&pkg=zip&m=blendbyte)
> 
> ![필히 Long Term 으로!](Java%20(26)%20-%20database,%20DBMS,%20SQL%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%206c58f9d3c83e4ed58c64e168361bccd0/Untitled%202.png)
> 
> 필히 Long Term 으로!
> 
> ![root p.w : 1111](Java%20(26)%20-%20database,%20DBMS,%20SQL%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%206c58f9d3c83e4ed58c64e168361bccd0/Untitled%203.png)
> 
> root p.w : 1111
> 
> 1. 찾기 > 서비스 에서 확인 가능
> 
> cmd > mysql -u root -p 확인 후, 경로 설정이 되어있지 않으면
> 
> 환경변수 설정 > 시스템변수 > Path
> 
> ![Untitled](Java%20(26)%20-%20database,%20DBMS,%20SQL%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%206c58f9d3c83e4ed58c64e168361bccd0/Untitled%204.png)
> 
> 다시 cmd > `mysql -u root -p` > password 입력
> 
> C:\Program Files\MariaDB 10.6\bin 확인 해보면,
> 
> mysql.exe (⇒ DBMS client) 설치 완료
> 
> mysqld.exe (⇒ DBMs) 설치 완료
> 
> ### 2. MySQL 사용자 추가 후 DataBase 정의
> 
> 사용자 추가는 1개 이상 가능
> 
> `CREATE USER '사용자아이디'@'원격호스트주소' IDENTIFIED BY '암호';`
> 
> 로컬 사용자 등록
> 
> `CREATE USER 'study'@'localhost' IDENTIFIED BY '1111';`
> 
> 원격 사용자 등록
> 
> `CREATE USER 'study'@'%' IDENTIFIED BY '1111';`
> 
> MySQL 데이터베이스 생성
> 
> `CREATE DATABASE studydb CHARACTER SET utf8 COLLATE utf8_general_ci;`
> 
> MySQL 사용자에게 데이터베이스 사용 권한 부여
> 
> `GRANT ALL ON studydb.* TO 'study'@'localhost';`
> 
> 원격에도 부여
> 
> `GRANT ALL ON studydb.* TO 'study'@'%';`
> 
> ### 3. SQL 작성법
> 
> 아래 경로 참조
> 
> ![Untitled](Java%20(26)%20-%20database,%20DBMS,%20SQL%20%E1%84%89%E1%85%A5%E1%86%AF%E1%84%8C%E1%85%A5%E1%86%BC%206c58f9d3c83e4ed58c64e168361bccd0/Untitled%205.png)
> 
> - PC와 Cloud간에 접근은, 보안상 Linux를 거쳐서 접근해야 한다.
>     - 다이렉트 접근 시, 보안상 심각한 문제가 발생할 수 있으며
>         
>         리눅스 우회가 필수적이므로, CLI 사용을 습관들이자. GUI는 추후에 선택사항.
>         
> 
> - key
>     
>     데이터를 구분할 때 사용하는 컬럼 집합
>     
>     두개 컬럼을 묶어서 데이터를 구문하는 식별자로 사용 가능
>     
>     eg. {name, tel}, {tel, basic_addr, gender, name} …
>     
> 
> ㄴ candidate key ( 후보키, 최소키 )
> 
> 최소 컬럼으로 줄인 키
> 
> ㄴ primary key ( 주키)
> 
> 후보키 중에서 DBMS 관리자가 사용하기로 결정한 키
> 
> ㄴ alternative key (대안키)
> 
> candidate key 중에서 primary key로 선택된 키를 제외한 나머지 키.
> 현재 주 키는 아니지만 주 키로 사용가능하여 대안키라고 하며, 보통 unique column (중복되지 않는 컬럼)으로 지정한다. “pk”
> 
> ㄴ artificial key (인공 키)
> 
> 주키로 사용할 적정한 컬럼이 없다면, 임의의(인공적으로) 컬럼을 만들어 key 컬럼으로 사용
> 
> eg. 게시글 일련번호
> 
> 현업에서 회원 데이터를 구분할 때, 
> 
> 이메일 → 변경 될 수 있고
> 
> 아이디 → 회원 탈퇴 후 활용되지 말아야 하기 때문에
> 
> ⇒ 회원일련번호 컬럼을 만들어 key 컬럼으로 사용
>