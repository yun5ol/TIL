# Java (27) - DBMS, SQL 계속

작업중: In progress
태그: Dev, 백엔드프로그래밍, 웹&모바일, 자바프로그래밍기초
학습일: 02/07/2023

## DML

### Commit / rollback

- Commit

thread 별로 임시 DB 존재,

commit 하지 않으면 (autocommit = false) 임시 DB에만 보관

- Rollback

임시 DB에 저장된 실행 결과를 제거

### Transaction

여러개의 데이터 변경 작업을 한 단위로 묶은 것

ㄴ insert, update, delete     ㄴ 모두 처리 또는 모두 취소

기업 업무 중에는 여러개의 작업을 한 단위로 다뤄야 하는 경우가 있다

eg. [주문 → 결제] → 주문완료( =commit)

이 transaction을 제어하는 문법이 commit & rollback

## DQL

projection : 추출할 colmn 선택

selection : 추출할 data 선택

## 

### 첨부파일 저장

1. DBMS에 파일 저장

- 파일을 꺼낼 때 DBMS를 경유하기 때문에 속도가 느리다
- 데이터베이스의 크기를 급격히 늘린다

“결론” 비효율적이다

1. DBMS에 파일 경로만 특정 컬럼에 저장
    - 데이터베이스가 급격하게 커지지 않는다.
    - 파일을 OS가 읽기 때문에 속도가 빠르다.

### 첨부파일과 테이블

- 첨부파일의 개수가 제한된다.
- 위처럼 개수가 한정되면 첨부파일이 없더라도 그 수 만큼 메모리를 차지한다.

따라서, 이를 극복하기 위해 여러개의 테이블로 분산, 저장한다.

### FK (foreign key)

위 방법의 문제점은 다른 테이블의 참조 여부에 따라 데이터가 깨질 수 있다.

따라서, 다른 데이터를 참조하는 경웅 해당 데이터의 존재 유무를 강제로 검사하는 문법이 “외부 키(foreign key)” 이다.

⇒ 다른 테이블의 데이터와 연관된 데이터를 저장할 때 무효한 데이터가 입력되지/지우지 않도록 제어하는 문법

- 무결성(integrity) 제약조건

<< entitiy = table >> “entity relationship diagram” (**ER D**iagram) 

부모테이블 / 자식테이블

PK / FK

⇒ 부모, 자식테이블 간 서로 참조 관계가 있으면, 데이터를 삭제할 수 없다