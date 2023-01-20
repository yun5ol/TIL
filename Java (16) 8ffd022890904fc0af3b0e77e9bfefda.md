# Java (16)

작업중: In progress
태그: Dev, 백엔드프로그래밍, 웹&모바일, 자바프로그래밍기초
학습일: 01/19/2023

## Wrapper 클래스

primitive type의 data를 포장하여 객체로 다룰 수 있게 해준다..

- 목적
    
    primitive type에 상관없이 Object 타입의 파라미터로 값을 받을 수 있다. ⇒ 객체로 다룰 수 있다.
    

**package** com.eomcs.basic.ex02;

### 오토박싱/오토언박싱

Boxing : primitive type의 값을 인스턴스에 담는다

- AutoBoxing
    
    `Integer.valueOf()` 로 Integer 객체 생성 후 주소를 저장
    

```java
Integer obj = 100; // ==> Integer.valueOf(100)
```

Unboxing : 인스턴스의 담긴 primitive 값을 다시 꺼내는 일

- AutoUnboxing
    
    `intValue()`로 인스턴스에 들어있는 값을 꺼내 int에 저장
    

```java
Integer obj = Integer.valueOf(300);
int i = obj; // ==> obj.intValue()
//즉 obj에 들어있는 인스턴스 주소가 i에 저장되는 것이 아니라,
//    obj 인스턴스에 들어 있는 값을 꺼내 i에 저장
```

### wrapper 객체 생성

1. wrapper 객체 생성은 new 대신, valueOf() 또는 auto-boxing을 이용한다.
    
    → new 연산자로 만들어진 생성자는 Heap 영역에 인스턴스를 생성
    
    → 데이터가 같은 값이더라도 다른 인스턴스를 생성한다.
    
    ⇒ 따라서, `valueOf()` 로 생성을 더 선호한다.
    
    > valueOf()
    > 
    > 
    > 정수 값이 `-128 ~ 127` 범위일 경우, 자주 사용되는 수이기 때문에
    > String 리터럴처럼 상수 풀에 Integer 객체를 생성한다. ⇒ 인스턴스가 같다.
    > 
1. 값 비교는 반드시 `equals()`를 사용한다.
    
    ==를 이용할 경우
    
    ⇒ 메모리 효율 관리를 위해 같은 값을 가지는 Integer 객체가 여러 개 존재하지 않게 한다.
    
    ⇒ 인스턴스가 같다 → 위 범위를 벗어나면 무조건 새 객체를 만든다.
    

## java.util.Date 클래스

### 생성자 활용

- `Date()` 기본 생성자
    
    toString 자동 호출되어 이렇게 출력된다 : `Thu Jan 19 10:03:43 KST 2023`
    
    Date d3 = **new** Date(`System.*currentTimeMillis*()`); // 같은 말이다
    
- `Date(long)`
    
    1970-01-01 00:00:00 부터 지금까지 경과된 밀리초를 출력한다 : `Thu Jan 01 09:00:01 KST 1970`
    
- [`java.sql.Date](http://java.sql.Date)` : util.Date을 상속받은 서브 클래스
    
    → 생성 방법 2가지 
    
    ```java
    // 1. java.sql.Date
        java.sql.Date d5 = new java.sql.Date(System.currentTimeMillis());
        System.out.println(d5);
    **// 패키지는 다르고 클래스명이 같을 때, 둘 다 import 할 수 없다. 
    // 따라서, 생성 시 앞에 표시해줘야 한다.**
    
    // 2. 간접적으로 객체를 생성하기
        java.sql.Date d6 = java.sql.Date.valueOf("2021-2-4");
        System.out.println(d6);
    ```
    

## java.util.Calendar 클래스

생성자가 있다하더라도 접근 권한이 없으면 호출할 수 없다. // protected

⇒ Calendar는 인스턴스 생성을 도와주는 별도의 클래스 메서드(스태틱 메서드)를 제공한다. *`getInstance*()`

→ 이렇게 하는 이유? 생성과정이 복잡!

```java
Calendar c1;
c1 = Calendar.getInstance();
System.out.println(c1.get(1)); //year
System.out.println(c1.get(2) + 1); //month는 0부터 시작이라 +1
System.out.println(c1.get(5)); //date
System.out.println(c1.get(10)); //hour
System.out.println(c1.get(9)); //am/pm
System.out.println(c1.get(12)); //minute
System.out.println(c1.get(13)); //second

// get(n)가 return 가능
// 하지만 추가 주석이 필요
// => 그냥 기재하자...!

System.out.println(c1.get(Calendar.YEAR));
System.out.println(c1.get(Calendar.MONTH) + 1);
System.out.println(c1.get(Calendar.DATE));
System.out.println(c1.get(Calendar.HOUR));
System.out.println(c1.get(Calendar.AM_PM));
System.out.println(c1.get(Calendar.MINUTE));
System.out.println(c1.get(Calendar.SECOND));
```

> 객체 생성 디자인 패턴 중 일부 소개 GoF(Gang of Four)의 23가지 디자인 패턴(design pattern) 
ex. *`getInstance*()`
> 
> 
> 
> 1. 팩토리 메서드(factory method)
>     - 인스턴스(객체)를 생성해주는 메서드이다.
>     - 인스턴스 생성 과정이 복잡할 경우, 인스턴스를 대신 생성해주는 메서드를 미리 정의해 둔다.
>     - 그래서 인스턴스가 필요할 때 마다 메서드를 호출하여 인스턴스를 리턴 받는다.
>         
>         ⇒ 복잡한 과정을 감췄다, 포장했다 ⇒ 캡슐화의 일부
>         
> 2. 싱글톤(singleton)
>     - 인스턴스를 한 개만 생성하도록 제한할 때 사용한다.
>     - 생성자를 private으로 처리하여 직접 인스턴스를 생성하지 못하도록 만든다.
>     - 메서드를 통해 인스턴스를 생성하도록 유도한다.

---

## 예외처리 Overview

### 예외 발생과 catch, 예외 리턴

**package** com.eomcs.exception.ex1;

1. 예외 발생

![Untitled](Java%20(16)%208ffd022890904fc0af3b0e77e9bfefda/Untitled.png)

2. 예외를 받는 try, catch 문법 활용

![Untitled](Java%20(16)%208ffd022890904fc0af3b0e77e9bfefda/Untitled%201.png)

1. 예외를 어디서 처리할 지는(어디서 catch할지) 옳고 그름의 문제가 아닌, 선택이다

![Untitled](Java%20(16)%208ffd022890904fc0af3b0e77e9bfefda/Untitled%202.png)

![Untitled](Java%20(16)%208ffd022890904fc0af3b0e77e9bfefda/Untitled%203.png)

### 예외 상황을 알리는 고전적인 방법

1. 리턴 값으로 오류 여부를 알려준다.
    
    문제점 > 정상적인 계산 결과도 오류로 취급할 수 있다.
    
    해결법 > 일반적인 리턴 값 대신 잘 흔하지 않은 값을 지정한다.
    
    ⇒ 그래도 고질적인 해결법은 될 수 없다.
    
2. 예외 처리 문법을 사용한다.

### 예외를 알리는 현대적인 방법

예외 상황이 발생했을 때 호출자에게 리턴 값으로 알려주는 것이 아니라, 따로 예외 정보를 던져준다.

1. **`throw** 예외 정보를 담은 객체;`
    
    위 객체는 반드시 **Throwable 객체여야** 한다.
    
    eg. `throw new Throwable(”예외내용”);`
    
    - 메서드 선언부에 Throwable 예외를 던지는 메서드임을 표시해야 한다.
        
        `리턴타입 메서드명() throws 예외타입, … {}`   예외타입 Throwable 클래스
        
        eg. int compute(…) throws Throwable {}   어떤 타입을 던지는지 표시한다
        
        ```java
        => throw [Throwable 객체];
        throw new String("예외가 발생했습니다!"); // 컴파일 오류!
        ```
        

### 예외를 받는 방법

try-catch-finally 문의 구조

```java
try { 
	예외가 발생할 수 있는 코드
} catch (Throwable e) { // 예외 객체를 받는 파라미터 (+ 서브클래스 포함)
	예외를 받아서 처리할 코드
} finally {
	정상코드 // 예외가 발생하든 정상적으로 수행하든 상관없이, 반드시 실행할 코드
}
```

---

## 문법 정리

**메서드를 실행하는 중에 예외가 발생했을 때 호출자에게 알려주는 문법 : throw
메서드를 호출하는 중에 예외를 받았을 때 처리하는 문법 : try~catch** 

> ⇒ 예외처리 문법의 의미
1) 메서드 실행 중에 예외 상황을 만났을 때 리턴 값으로 알려주는 방식의 한계를 극복하기 위해
2) 예외가 발생하더라도 시스템을 멈추지 않고 적절한 조치를 취한 후 계속 실행하기 위해
> 

### 예외상황 호출자에게 알리기

- Throwable 계층도
    
    `Throwable`
    
    ㄴ `Error : 시스템 예외`
    
    - JVM이 발생시키는 심각한 예외
    - App 에서 던지면 안된다
    - **정상적인 실행상태로 복귀가 불가능** → 간단한 예외 처리 후 **즉시 종료**된다
        
        ⇒ 현재까지 작업 내용 임시 저장 or
        
        ⇒ 사용자에게 안내 메시지 출력 or
        
        ⇒ 오류 기록 남김 정도의 조치만 가능
        
    
    ㄴ `Exception : 어플리케이션 예외`
    
    - App.에서 발생시키는 예외
    - 적절한 조치를 취한 후 정상적인 실행상태로 복귀 가능
    - 개발자가 던지는 예외
    - 호출한 쪽에서 반드시 try~catch 로 받아야 한다
    
     ㄴ`RuntimeException : Unchecked Exception`
    
    - try~catch 로 받지 않아도 되며, 그럴 경우 상위 호출자에게 던져진다
        
        ⇒ 해당 메서드를 예외를 던지는지 검사하지 않는 예외
        
    - 예외처리 편이성에 좋다

<aside>
📍 예외를 던질 때 Throwable 클래스를 직접 사용하지 말라!
그 하위 클래스, 특히 애플리케이션 오류를 의미하는 **Exception 클래스를 사용하라.**

</aside>

- Exception
    - 예외를 던질 때 반드시 메서드 선언부에 어떤 예외를 던지는지 지정해야 한다.
    - 메서드에서 발생되는 예외는 메서드 선언부에 모두 나열해야 한다.
        
        > 공통 분모를 사용하여 퉁치는 방법
        ⇒ 메서드에서 발생하는 예외의 **공통 수퍼 클래스**를 지정한다
        → **그러나 호출자에게 어떤 오류가 발생하는지 정확하게 알려주는게 유지보수에 좋다.**
        > 
    - RuntimeException
        
        Exception의 서브 클래스임에도 RuntimeException 객체를 던질 경우,
        메서드 선언부에 예외를 던진다고 표시하지 않아도 된다.
        → 보통 스텔스 모드(비유!)로 예외를 전달할 때 사용된다.
        

### 던지는 예외 받기

> Exception
> 
- 예외를 던질 수 있다고 선언된 메서드를 호출할 때, 그 예외 상황에 대한 처리를 하지 않으면 컴파일 오류가 발생한다.
- 여러 개의 예외를 받을 때 수퍼 클래스 변수로 먼저 받지 말라!
그러면 그 클래스의 모든 서브 클래스 객체도 다 받게 된다.
- 다형적 변수의 특징을 이용하여 여러 예외를 한 catch에서 받을 수 있다.
    
    ```java
    catch (Exception e) {
    ...
    } catch (RuntimeException | SQLException | IOException e) {
      // OR 연산자를 사용하여 여러 개의 예외를 묶어 받을 수 있다.
      //
    } catch (Exception e) {
    ```
    

> Error
> 
- 가능한 Error 계열의 시스템 예외를 받지 않는다.
⇒ 시스템 예외는 당장 프로그램을 정상적으로 실행할 수 없는 상태일 때 발생한다.
⇒ 시스템을 멈출 수 밖에 없다.

<aside>
📍 Throwable 변수로 예외를 받지 말라!

**catch** 문에 무심코 Throwable 변수로 선언하면 시스템 오류인 Error 까지 받기 때문에,

JVM에서 발생된 오류에 대해서도 예외 처리를 하는 문제가 발생한다.

시스템 오류는 애플리케이션에서 처리할 수 없다.

결론

Exception 계열의 애플리케이션 예외만 처리하라.

</aside>

> cf. 예외 처리 책임을 상위 호출자에게 위임 가능
> 
> 
> 해당 클래스에서 try~catch 로 받지 않는 경우, 상위 호출자로 위임되어 main(), JVM까지 전달될 수 있다.
> 
> → 하지만  VM은 main()에서 던지 예외를 받는 순간 즉시 실행을 멈추므로 바람직하지 않다.
> 

### 예외 처리 후 처리 작업

> finally
> 
- 정상적으로 실행하든, 아니면 예외가 발생하여 **catch** 블록을 실행하든, **finally** 블록은 무조건 실행한다.
    
    ⇒ 즉 **try** ~ **catch** ~ 블록을 나가기 전에 반드시 실행한다.
    
- finally 블록과 자원 해제
    
    **package** com.eomcs.exception.ex3; 0610
    
    - 항상 자원을 사용한 후 해제시키는 것을 습관적으로 해야 한다.
        
        → 문제는 close()를 호출하기 전에 예외가 발생한다면, 제대로 자원을 해제시키지도 못한다는 것이다.
        
        해결법 > **finally** 블록을 사용하는 것이다.
        
        ⇒ **finally의 존재 이유**
        

```java
finally {
      // 이렇게 정상적으로 실행되든 예외가 발생하든 상관없이
      // 자원해제 같은 일은 반드시 실행해야 한다.
      keyScan.close(); ...
```

- **자동** 자원 해제 (실무용)
    
    **`try**-with-resources`  eg. try (Scanner keyScan = new Scanner(System.*in*)) {
    
    ⇒ 굳이 finally 블록에서 close()를 직접 호출할 필요없이 자동 처리된다.
    
    <aside>
    📍  단 java.lang**.AutoCloseable** 구현체에 대해서만 가능하다!
    
    </aside>
    
    - 문법
        
        `try (java.lang.AutoCloseable 구현체) {...}` eg. 해당 구현체: FileReader
        
    - 해당 구현체는 클래스명 옆에 아래와 같이 선언해줘야 한다.
        
        `implements AutoCloseable` eg. static class C implements AutoCloseable { …
        
    - 단, **AutoCloseable** 구현체는 **예외가 발생하면** try{} 블록을 나가기 전에 close()가 먼저 호출된다.

### 예외 던지고 받기

- Exception 계열의 예외를 상위 호출자에게 전달할 때, 호출 경로에 있는 모든 메서드에 어떤 예외인지 선언해야 한다. eg. `**throws** Exception {` …
    
    ⇒ 단, 메서드에 예외를 받는 코드가 있을 경우, 선언부에 지정할 필요 없음
    
    → 예외가 JVM까지 전달되지 않도록 할 것 ⇒ 실행 종료 되버리니깐
    
- 위를 해결하는 방법 > `RuntimeException`
    
    Error 예외 처럼 상위 호출자에게 선언부 없이, 자동 전달
    
    ⇒ 예외 처리를 하고 싶은 곳에, catch 블럭으로 받아 처리해주면 된다.
    
- RuntimeException
    
    Exception의 서브 클래스임에도 RuntimeException 객체를 던질 경우,
    메서드 선언부에 예외를 던진다고 표시하지 않아도 된다.
    
    > 해당 계열 eg
    > 
    > 
    > Integer.parseInt() => NumberFormatException 이 발생할 수 있다.
    > Data.valueOf() => IllegalArgumentException 이 발생할 수 있다.
    > 
    > = */*throws NumberFormatException, IllegalArgumentException*/* {.. 선언부에 생략 가능 
    > 
    > = **catch** (RuntimeException e) { .. 퉁치기 가능
    > 
- 예외의 의미를 직관적으로 파악할 수 있도록 별도의 예외 객체를 만들어 던진다.
⇒ 게시물 예외를 직관적으로 알 수 있는 클래스를 만든다.
eg. 그 클래스가 BoardException
    - 그리고, 별도 객체에 상속됨을 표기한다.
        
        **public** **class** BoardException **extends** RuntimeException { …
        
    - 이 클래스는 생성자가 호출될 때 그와 대응하는 수퍼 클래스의 생성자를 호출하는 일
        
        외에는 다른 작업을 수행하지 않는다.
        
        → 그럼 왜 RuntimeException을 상속 받았는가?
        이 클래스는 기존의 예외 클래스 기능을 확장하기 위함이 아니라,
        의미있는 이름을 가진 예외 클래스를 만드는 것이 목적이다.
        ⇒ 즉 예외가 발생했을 때 클래스 이름으로 어떤 예외인지 쉽게 추측할 수 있도록 하기 위함이다.
        ⇒ 일종의 분류표로서 사용한다.
        

