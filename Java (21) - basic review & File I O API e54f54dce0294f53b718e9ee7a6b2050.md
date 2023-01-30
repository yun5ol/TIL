# Java (21) - basic review & File I/O API

작업중: In progress
태그: Dev, 백엔드프로그래밍, 웹&모바일, 자바프로그래밍기초
학습일: 01/30/2023

# Collection API

(객체지향 : 인터페이스와 클래스간의 관계 파악 중요)

각 클래스를 다루는 3개의 인터페이스 정의

- List ↘
    - Collection  (List와 Set의 공통 부분을 뽑은 인터페이스)
- Set ↗
- Map

| List | 순서O, 중복O |
| --- | --- |
| Set | 순서X, 중복X |
| Map | 키(key)와 값(value)의 쌍으로 이루어짐
순서X, 중복:키X/값O |

> [Object 클래스](https://www.notion.so/Object-bb284c39fc3e4a29aff5f088909b2cce) - Object 클래스 참조
> 
> 
> ```java
> System.out.println(obj.toString());
> System.out.printf("%08x, %1$d\n", obj.hashCode());
> System.out.println(obj.equals("Hello"));
> 
> ---------------------------------
> 
> Object 클래스의 주요 메서드
>  1) toString()
>     => 클래스이름과 해시코드를 리턴한다.
>  2) equals()
>     => 같은 인스턴스인지 검사한다. 
>  3) hashCode()
>     => 인스턴스를 식별하는 값을 리턴한다.
>  4) getClass()
>     => 인스턴스의 클래스 정보를 리턴한다.
>  5) clone()
>     => 인스턴스를 복제한 후 그 복제 인스턴스를 리턴한다.
>  6) finalize()
>     => 가비지 컬렉터에 의해 메모리에서 해제되기 직전에 호출된다.
> ```
> 

## List 관련 클래스 계층도 (hierarchy)

![Untitled](Java%20(21)%20-%20basic%20review%20&%20File%20I%20O%20API%20e54f54dce0294f53b718e9ee7a6b2050/Untitled.png)

### 0. List 인터페이스

1. 순서대로
2. 데이터중복 허용

- 주요 메서드와 메서드 특징
    - 객체가 같은지 비교할 때 equals()를 이용한다
    - 하지만 오버라이딩은 equals와 hashCode 둘 다 한다.
        - 영향을 끼치진 않지만, hashSet에 쓰일 수 있으니깐

### ArrayList

배열을 이용하여 목록 관리

![Java 17 API ](Java%20(21)%20-%20basic%20review%20&%20File%20I%20O%20API%20e54f54dce0294f53b718e9ee7a6b2050/Untitled%201.png)

Java 17 API 

## Set 관련 클래스 계층도

![Untitled](Java%20(21)%20-%20basic%20review%20&%20File%20I%20O%20API%20e54f54dce0294f53b718e9ee7a6b2050/Untitled%202.png)

### 1. Set

⇒ 집합 개념

1. 중복 불가
2. 순서 무관

- 주요 메서드와 메서드 설명
    - 객체가 같은지 비교할 때 equals()와 hasCode() 모두를 이용한다
    - 비교할 필드의 범위는 개발자가 선택

### HashSet

![Untitled](Java%20(21)%20-%20basic%20review%20&%20File%20I%20O%20API%20e54f54dce0294f53b718e9ee7a6b2050/Untitled%203.png)

## Map 관련 클래스 계층도

![Untitled](Java%20(21)%20-%20basic%20review%20&%20File%20I%20O%20API%20e54f54dce0294f53b718e9ee7a6b2050/Untitled%204.png)

### 2. Map

1. 키와 값의 쌍으로 이루어진 데이터의 집합
2. 순서 X
3. 중복 - 키 X / 값 O

### HashMap

속도가 빠른게 가장 큰 장점, 특징

- Map이 리턴하는 것은 set

→ 이 안에 Entry

→ Entry 안에 key, value

> entrySet()
> 
> 1. key, value가 들어있는 set 객체 
> 2. value ⇒ Map.entry
>     1. Map 인터페이스 안에 Entry라는 inner 인터페이스 (nested interface)
>     2. 따라서, Map.entry
> 3. Entry 안에 key, value가 있다.
>     
>     eg. <Entry <String,Member>>
>     

### HashMap vs HashTable

1. Map : value는 null 지원
    
    Table : 둘 다 미지원
    
    key : null 허용 안됨
    
    Map은 value : null 허용
    
2.  동기화 지원
    1. 여러 thread가 동시에 접근하더라도 데이터가 깨지지 않음
3. 대신 속도는 HashMap이 빨라 (조건검사 없어서)

⇒ HashMap이 더 일상적

---

## 26. 바이너리 데이터 입출력

1. 주고받는 데이터는 주로 바이트배열이며, 객체에서 변환이 필요하다
2. Board 객체가 여러개일 경우, 경계 구분이 필요
    
    따라서 읽는 순서는 배열크기 → 데이터 → Board 객체로 변환 → List 배열에 담는다 : get()/add()
    

### Myapp Overview

바이너리데이터 : 바이트배열

1. 바이너리데이터를 출력할 도구 준비
    
    `FileOutputStream`
    
2. 예외 설정
3. 목록에서 Board 객체를 꺼내 바이트 배열로 만들고 출력한다

…

- String → byte[]

getBytes()

arrayCopy()

byte[] 형태의 데이터를 자르거나 연접하는 메서드

```java
System.arraycopy(strBytes, 0, bytes, 2, strBytes.length);
// 복사하고자 하는 원본 소스
// 원본 소스에서 어느 부분부터 읽어올지 위치 지정
// 복사할 소스
// 복사본에서 자료를 받을 때, 어디부터 써서 시작 위치 지정
// 원본에서 복사본으로 데이터를 읽어서 쓸 데이터의 길이 = 원본소스(가져오는) 길이
```

![Untitled](Java%20(21)%20-%20basic%20review%20&%20File%20I%20O%20API%20e54f54dce0294f53b718e9ee7a6b2050/Untitled%205.png)

- byte[] → String

InputStream

read(byte[] b, int off, int len) 

입력 스트림으로부터 len개의 바이트만큼 읽고

매개값으로 주어진 바이트 배열 b[off]부터 len까지 저장

실제로 읽은 바이트 수인 len개를 리턴

len개를 모두 읽지 못하면 실제로 읽은 바이트 수 리턴

[[ JAVA ] - 입력 스트림과 출력 스트림(1) : InputStream - read() 메서드 / read(byte[] b) 메서드](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=rain483&logNo=220625042360)

*readString*(in)

ByteArrayInputStream()

바이트 배열에서 데이터를 읽는 도구

- fileoutputstream : 데이터를 파일에 바이트 스트림으로 저장하기 위해 사용

### FileOutputStream/ FileInputStream 도구 사용법

<aside>
📍 개발자 입장에서 파일 읽어드리는게 Input

</aside>

- 다루는 데이터는 주로 바이트배열
    - 이때, 객체에서 바이트배열을 변환하는데,

| FileOutputStream | FileInputStream |
| --- | --- |
|  |  |
|  |  |