# Java (32)

작업중: In progress
태그: Dev, 백엔드프로그래밍, 웹&모바일, 자바프로그래밍기초
학습일: 02/14/2023

## 39.  멀티스레드와 DB커넥션 관리

순차접속 → 동시접속 : 멀티스레드 활용 위해 요청 처리 코드를 별도 스레드로 관리

### 현재 멀티스레드와 DB커넥션을 공유할 때 문제점

- 한 클라이언트가 rollback을 요청하면, 공유 중인 DB 커넥션 Thread에 보관된 다른 클라이언트의 요청까지 모두 취소된다.
- **따라서, 멀티스레드 환경에서는 DB커넥션을 공유하지 않는다.**

### 해결

ConnectionFactory를 생성하여 thread별로 connection 객체를 킵해준다

## 40.  DB 커넥션 풀을 이용한 Connection 재사용

### Thread 별 Connection 관리의 문제점

스레드 마다 매번 DB커넥션 객체 생성 필요 

1. 가비지가 많이 생성
2. 커넥션 되는데 시간 소요

### Connection Pool 도입

⇒ pooling 기법

GoF의 ‘Flyweight’ 디자인 패턴

- ConnectionFactory는 ConnectionPool에서 생성 또는 리턴되는 connection을 사용한다
    - getConnection()
    - closeConnection()
    - returnConnection()
        - return 해주지 않으면, 새로 생성해야 하는건 마찬가지
    - conFactory.closeConnection()
        - 현재 스레드가 갖고있는 커넥션 객체를 ConnectionPool에 반납한다

<aside>
📍 위 모든 과정의 자동화 “java.util.DataSource

</aside>

## 41.  PreparedStatement 를 이용한 SQL 삽입 공격 방지

### SQL 삽입 공격 체험

"update app_board set title='%s', content='`%s`' where board_id=%d”

`hul', view_cnt=20000, created_date='2024-05-05', pwd='d`

⇒ 아래와 같다

update app_board set title='xxx', content='hul', view_cnt=20000, created_date='2024-05-05', pwd='d' where board_id=3

 

### 해결

- preparedStatement 활용
    - in파라미터
    - executeQuery 자동 close를 위한 try문

## 42. Mybatis SQL Mapper

- Mybatis API 사용준비

`implementation 'org.mybatis:mybatis:3.5.11'`

1. Mybatis 설정 파일 준비
    
    resources/bitcamp/myapp/conf/mybatis-config.xml
    
    ```java
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE configuration
      PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
      "https://mybatis.org/dtd/mybatis-3-config.dtd">
    <configuration>
      <environments default="development">
        <environment id="development">
          <transactionManager type="JDBC"/>
          <dataSource type="POOLED"> 
            <property name="driver" value="org.mariadb.jdbc.Driver"/>
            <property name="url" value="jdbc:mariadb://localhost:3306/studydb"/>
            <property name="username" value="study"/>
            <property name="password" value="1111"/>
          </dataSource>
        </environment>
      </environments>
      <mappers>
        <mapper resource="bitcamp/myapp/mapper/BoardMapper.xml"/>
      </mappers>
    </configuration>
    ```
    

<aside>
📍 <environments default=*"development"*>

</aside>

1. SQL Mapper 파일 준비
    
    resources/bitcamp/myapp/mapper/BoardMapper.xml
    
    ```java
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE mapper
      PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
      "https://mybatis.org/dtd/mybatis-3-mapper.dtd">
    <mapper namespace="BoardMapper">
    
    <select id="findAll" resultType="bitcamp.myapp.vo.Board">
      select
        board_id as no, // 프로퍼티 명과 동일하
        title, 
        created_date as createdDate, 
        view_cnt as viewCount 
       from 
        app_board 
       order by 
        board_id desc
      </select>
    
    </mapper>
    ```
    
2. Mybatis 설정 파일을 읽을 때 사용할 입력 스트림 객체 준비 # ServerApp
3. SqlSessionFactoryBuilder 준비
4. builder를 이용하여 SqlSessionFactoryBuilder 객체 생성

… 내일 이어서