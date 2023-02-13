# Java (31)

작업중: In progress
태그: Dev, 백엔드프로그래밍, 웹&모바일, 자바프로그래밍기초
학습일: 02/13/2023

## Desktop VS Application

Application 이점

 1. 

1. 

## 38. 트랜잭션 다루기 ⇒ 포함관계로 변경 (자식테이블로)

### 포함 관계와 배타적 관계

eg. ERD 참고

포함관계 (inclusive) : 회원 데이터가 학생과 강사 데이터와 동시에 관련될 수 있다

⇒ 즉 강사이면서 학생일 수 있을 때 이런 관계로 표현 = 로그인 페이지가 동일하다 ex.인프런

배타적관계 (exclusive) : 회원 데이터는 학생, 매니저, 강사 중 한 개의 데이터하고만 관련될 수 있다

⇒ 강사이면서 매니저가 되려면 따로 추가 가입을 해야한다 = 아이디가 달라진다

### Dao와 테이블

- 식별관계 (identifying relationship)
- member_id (pk)
- member (pk=fk)

> Handler - DAO - Table
> 
> - owner : 변경 권한을 가짐 (insert/update/delete)
>     - 보통 하나의 dao가 하나의 table에 ownership을 가진다
>     - 이때, 하나의 table에 자식table이 있다면, 그 자식 테이블의 ownership 까지 가진다
>         
>         ⇒ 관리가 용이할 때
>         
>     - 하나의 dao가 다른 table의 ownership을 가질 수 없다
>         
>         why? 변경에 대한 추적 & 책임소재가 불분명하다
>         
>         ⇒ 다만 viewer(select)는 가능하다
>         
> - 하나의 handler가 여러 dao를 호출 할 수 있다
> - handler 간의 호출은 비추
>     
>     why? 종속 관계가 생성→업무로직이 의존적 변경→재사용성이 낮아진다
>     
>     ⇒ dao 간 호출도 마찬가지
>     

---

비밀번호 256비트로 변

update app_member set pwd = sha(’1111’,256);

join할 때는 테이블 별명 필요

select 에는 불필요