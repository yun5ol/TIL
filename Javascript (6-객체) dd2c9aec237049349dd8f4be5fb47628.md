# Javascript (6-객체)

교재: Do it! 웹표준의정석
작업중: In progress
태그: Dev, 웹&모바일, 웹프로그래밍기초
학습일: 12/12/2022

## 객체

### 프로퍼티 추가

생성자를 이용하여 기본 객체를 준비한 후, 필요한 프로퍼티 (변수와 함수, 객체)를 추가할 수 있다.

> **객체 생성**
> 
> 
> ```jsx
> var obj = new Object(); // new : 빈 객체 생성
> 
> // 생성자에 null을 주면 완전한 빈 객체 생성	
> var obj = Object.create(null); // ==> 빈객체(표)생성
> 						//	= new		생성자
> 
> var obj = Object.create(Object.prototype); // ==> 1) 빈객체 생성
> 								= new Object()	// 2)프로토타입으로 지정된 생성자를 통해 기본 프로퍼티 추가		
> ```
> 
> **생성자** (constructor) 
> 
> cf. 자바, 자바스크립트 각각 생성자의 의미가 다르다.
> 
> ```jsx
> new Object();
>   // = 생성자 : 빈 객체에 프로퍼티를 준비
> 
> // cf. 
> // new : 빈객체 생성 (표)
> // Object() : key에 프로퍼티 준비
>  
> // => 이렇게 생성된 객체 안의 기본 함수들
> 	
> console.log(obj.toString()); // 객체를 문자열로 출력
> console.log(obj.valueOf()); // 객체를 그대로 출력
> console.log(obj.hasOwnProperty("toString"));
> console.log(obj.hasOwnProperty("hashCode"));
> ```
> 
> **hasOwnProperty(”프로퍼티명”)**
> 
> 개발자가 추가시킨 프로퍼티인지 검사 (아니면 생성자가 추가)
> 
> ```jsx
> // eg.
> var obj = new Object();  
> console.log(obj.hasOwnProperty("toString"));
> // false = 생성자가 추가
> 
> ↕
> 
> obj.title = "제목입니다.";
> obj["content"] = "내용입니다.";
> obj['viewCount'] = 120;
> 
> // 물론 그 값으로 함수 객체의 주소를 저장할 수 있다.
> // 객체의 변수 안에 함수 주소가 들어있으면, 그 함수 주소를 꺼내서 함수 처럼 호출할 수 있다.
> function f1(a, b) {
>   return a + b;
> }
> obj.plus1 = f1; // 함수명은 그 자체가 함수 객체의 주소를 갖고 있는 변수이다.
> obj.plus2 = function(a, b) {
>   return a + b;
> };
> 
> obj.plus3 = (a, b) => console.log("합계=", a + b); // arrow function
> 
> console.log(obj.hasOwnProperty("title"));  // true
> console.log(obj.hasOwnProperty("content")); // true
> console.log(obj.hasOwnProperty("viewCount")); // true
> console.log(obj.hasOwnProperty("plus1")); // true
> console.log(obj.hasOwnProperty("plus2")); // true
> console.log(obj.hasOwnProperty("plus3")); // true
> ```
> 

### 프로퍼티 추가 2

프로퍼티는 일반 숫자, 문자열, 논리값 또는 함수(주소)와 객체까지 저장할 수 있다.

cf. 함수도 객체다.

```jsx
var obj = new Object();

obj.name = "홍길동";
obj.f1 = () => console.log("f1()....");

var obj2 = new Object();
obj2.v1 = 100;
obj2.v2 = true;
obj2.v3 = "문자열";
obj2.v4 = () => console.log("v4()....");

// 이렇게 프로퍼티의 값으로 다른 객체의 주소를 저장할 수 있다.
obj.other = obj2;

// 객체의 프로퍼티 값 꺼내기 // 저장할 때 사용한 프로퍼티 이름으로 호출
console.log(obj.name);
console.log(obj.other.v1); // 자바의 OGNL(Object Graph Navigation Language)와 비슷하다.
console.log(obj.other.v2);  
console.log(obj.other.v3);

// 객체의 함수 호출
obj.f1();
obj.other.v4();
```

> 객체가 다른 객체를 포함하는 경우
> 
> 
> ![Untitled](Javascript%20(6-%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6)%20dd2c9aec237049349dd8f4be5fb47628/Untitled.png)
> 

### this

같은 객체에 소속된 멤버 (변수나 함수, 객체)를 사용하려면 참조변수 this를 반드시 붙여야 한다.

⇒ 자바에서는 생략 가능, 자바스크립트는 불가

![Untitled](Javascript%20(6-%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6)%20dd2c9aec237049349dd8f4be5fb47628/Untitled%201.png)

```jsx
obj.toString = function() {
	// 자바와 달리 객체의 프로퍼티 변수를 사용할 때는 반드시 this를 붙여야 한다.생략하면 안된다.
	return this.name + "," + this.kor + "," + this.eng + "," + this.math; 
};   // 위 toString 객체를 의미

obj.toString = function() {
var name = "okok"
return this.name + "," + this.kor + "," + this.eng + "," + this.math;
}; // name은 함수 가장 가까운 정의를 찾아 호출
console.log("----------------------");

// 외부에 정의된 것 호출
window.name = "nono";
// 또는 var name = "nono";
console.log("----------------------");

obj.toString = function() {
return name + "," + this.kor + "," + this.eng + "," + this.math;
}; 
// name은 this를 제외하면, window.name 이 호출됨

/*
정리
1. this로 지정된 name 출력
2. this 없으면 함수 가장 가가운 정의를 찾아 호출
3. 외부 또한 마찬가지
4. 둘 다 없으면 window.name 호출
*/
```

### {} 객체 생성 : 객체 리터럴

{}은 기본 **객체를 생성**하는 단축 문법이다. = 객체 리터럴 (객체를 코드로 표현하는 방법)

```jsx
var obj = {}; //new Object(); "같은거다"
```

> **객체에 프로퍼티 추가할 때도 사용된다. {}**
> 
> 
> ```jsx
> var obj = {}; //new Object();
> 
> obj.name = "홍길동";
> obj.kor = 100;
> obj.eng = 90;
> obj.math = 80;
> obj.sum = function() {
> 	return this.kor + this.eng + this.math; // 항상 같은 객체의 멤버를 가리킬 때는 this를 붙여야 한다.
> };
> obj.aver = function() {
> 	return this.sum() / 3; // 항상 같은 객체의 멤버를 가리킬 때는 this를 붙여야 한다.
> };
> ```
> 

양쪽 다 같다.

```jsx
**// 실무에서 이거 더 많이 쓴다.**

var obj = {
	"name": "홍길동",
	'kor': 100,
	eng: 90, // 자바스크립트 문법 : 그냥 적는걸로 추천
	math:80,
	sum: function() {
	    return this.kor + this.eng + this.math;
	},
	aver: function() {
	    return this.sum() / 3;
	}
}
```

> **{}을 이용하여 기본 객체에 함수를 추가하는 또 다른 방법**
> 
> 
> ```jsx
> /*
>   sum: function() {
> 	  return this.kor + this.eng + this.math;
>   },
> */
> ```
> 

양쪽 다 같다.

```jsx
	sum() {
	    return this.kor + this.eng + this.math;
	},
	aver() {
	    return this.sum() / 3;
	}
```

### **{} 문법과 arrow function**

arrow function을 객체의 프로퍼티로 등록할 때,

**arrow function에서 this**는 소속된 객체가 아니라 **window 객체**를 가리킨다.

그의 반해 **일반 함수나 익명 함수**에서 사용하는 this는 자신이 **소속된 객체**를 가리킨다.

---

생성자의 필요성…

코드를 계산하는 방법과 줄이는 방법…

### 객체 생성과 초기화

#10-1

객체 주소를 담기 위해 낱개 정의

```jsx
var s1 = new Object();
s1.name = "홍길동";
s1.kor = 100;
s1.eng = 100;
s1.math = 100;
s1.sum = s1.kor + s1.eng + s1.math;
s1.aver = s1.sum / 3;
...
```

#10-2

객체 주소를 담기 위해 배열 사용 “배열객체 생성”

why? 반복문 사용 가능

```jsx
var scores = []; //new Array();
... // [0] [1] [2] 처럼
scores[2] = {}; // new Object();
scores[2].name = "임꺽정";
scores[2].kor = 80;
scores[2].eng = 80;
scores[2].math = 80;
scores[2].sum = scores[2].kor + scores[2].eng + scores[2].math;
scores[2].aver = scores[2].sum / 3;

for (var score of scores) {
    console.log(score.name, score.kor, score.eng, score.math, score.sum, score.aver);
}
```

#10-3 

함수를 이용해 객체 생성

eg. **createScore 함수**

<aside>
💡 팩토리 메서드 패턴 (factory method design patterns) by GoF(Gang of Four)
이렇게 함수를 통해 객체를 생성하는 기법.
객체 생성 과정이 복잡할 경우 직접 객체를 생성하고 초기화시키기 보다,
함수를 통해 객체를 생성하고 초기화시키는 것이
코드를 더 간결하게 만든다.

</aside>

```jsx
function createScore(name, kor, eng, math) { // 객체를 만들어 주는 함수
	const obj = new Object();
	obj.name = name;
	obj.kor = kor;
	obj.eng = eng;
	obj.math = math;
	obj.sum = kor + eng + math;
	obj.aver = obj.sum / 3;
	return obj;
}

var scores = []; // new Array();
scores[0] = createScore("홍길동", 100, 100, 100);
scores[1] = createScore("임꺽정", 90, 90, 90);
scores[2] = createScore("유관순", 80, 80, 80);

for (var score of scores) {
    console.log(score.name, score.kor, score.eng, score.math, score.sum, score.aver);
}

console.log("---------------------------------------------");

// 아직 부족한 점!
// => 특정 과목의 점수가 바뀌면 다시 합계와 평균을 계산해야 한다.
scores[2].kor = 100;
scores[2].sum = scores[2].kor + scores[2].eng + scores[2].math;
scores[2].aver = scores[2].sum / 3;

for (var score of scores) {
    console.log(score.name, score.kor, score.eng, score.math, score.sum, score.aver);
}
```

#10-4

객체 프로퍼티에 함수 저장

객체의 값을 다루는 함수를 객체에 추가한다.

```jsx
function createScore(name, kor, eng, math) {
	var obj = new Object();
	obj.name = name;
	obj.kor = kor;
	obj.eng = eng;
	obj.math = math;
	obj.sum = function() {
		return this.kor + this.eng + this.math;
	};
	obj.aver = function() {
		return this.sum() / 3;
	};
	return obj;
}

var scores = []; //new Array();
scores[0] = createScore("홍길동", 100, 100, 100);
scores[1] = createScore("임꺽정", 90, 90, 90);
scores[2] = createScore("유관순", 80, 80, 80);

for (var score of scores) {
    console.log(score.name, score.kor, score.eng, score.math,
            score.sum(), score.aver()); // 함수를 호출해서 꺼낸다
}

console.log("--------------------------------------------");

// 과목의 점수를 변경하더라도 합계와 평균은 다시 계산되기 때문에 편하다!
scores[2].kor = 100;

for (var score of scores) {
    console.log(score.name, score.kor, score.eng, score.math,
    		score.sum(), score.aver());
}

// 아직 부족한 점!
// => 객체가 만들어질 때 마다 같은 함수가 중복 생성됨, 메모리낭비
```

#10-5 > 다시

내부에서 객체 생성

#10-6 > 다시

외부에서 객체 생성 > 내부의 this.객체가 값을 받는다.

객체를 return 할 필요 x

> **new 사용법**
> 
> 
> ```jsx
> new createScore("" ...);
> 
> /*
> 1) 빈 객체 생성 (new)
> 2) Object() 자동 호출
> 3) createScore 실행
> */
> ```
> 

![Untitled](Javascript%20(6-%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6)%20dd2c9aec237049349dd8f4be5fb47628/Untitled%202.png)

#10-7

생성자 역할을 하는 함수의 이름은 대문자로 시작

생성자 이름은 객체의 용도를 표현하는 명사 형태로 작성

```jsx
// createscore = Score
function Score(name, kor, eng, math) {
...
```

위와 같이 함수 이름을 대문자로 시작하면, 생성자 역할을 하는 함수임을 직관적으로 알 수 있어 유지보수에 좋다.

**따라서, 생성자 이름은 모두 대문자, 명사구로 표현됨**

#10-8

객체에 대해 공통으로 사용하는 함수 공유하기

1) 생성자는 값만 저장하자

2) 객체의 값으로 돌아가는 함수 정의는, 별도의 보관소에 저장한다. (객체 내가 아니라)

How? prototype!

> **생성저와 prototype**
> 
> 
> Score() (생성자)가 초기화시킨 모든 객체가 공유하는 프로퍼티
> 
> 프로토타입은 함수나, 변수 모두 담을 수 있다.
> 
> ![Untitled](Javascript%20(6-%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6)%20dd2c9aec237049349dd8f4be5fb47628/Untitled%203.png)
> 

```jsx
eg.
// 1) 자바스크립트 함수는 객체이다. 즉 "함수 = 객체 + 함수코드" 이다.
// 2) 각각의 함수 객체는 prototype 이라는 공용 저장소를 갖고 있다.
// 3) prototype에 저장된 프로퍼티는 그 함수를 통해 초기화된 모든 객체가 공통으로 사용할 수 있다.
Score.prototype.sum = function() { ...
}
```

### 생성자를 정의하는 방법

생성자는 문법 따로 없다.

> **생성자와 일반함수**
> 
> 
> ```jsx
> // => new 명령 다음에 함수를 호출하면 생성자로서 역할한다.
> var obj1 = new f1();
> 
> /* 
> 1) new 명령어로 빈 객체 생성
> 2) objcet() 호출 > toString... 등 준비
> 3) f1() 호출	
> 
> 리턴 하는 것은, new가 생성한 객체 주소를 리턴
> */
> 
> console.log(obj1);
> console.log("-----------------------");
> 
> // new 명령없이 호출하면 일반 함수로 취급된다.
> var obj2 = f1();
> console.log(obj2);
> ```
> 

### 일반 함수로 동작할 때와 생성자로 동작할 때의 차이

11-2~

11-4~

> **생성자와 Object()**
> 
> 
> ![Untitled](Javascript%20(6-%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6)%20dd2c9aec237049349dd8f4be5fb47628/Untitled%204.png)
> 
> ![Untitled](Javascript%20(6-%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6)%20dd2c9aec237049349dd8f4be5fb47628/Untitled%205.png)
> 
> ```jsx
> console.log(obj1.toString());  // Object.prototype.toString() = 생성자 프로토타입에 있는
> console.log(obj2.toString());  // Object.prototype.toString();
> console.log(obj3.toString());  // Object.prototype.toString();
> ```
> 

11-5

> **생성자를 상속 받기**
> 
> 
> ![Untitled](Javascript%20(6-%E1%84%80%E1%85%A2%E1%86%A8%E1%84%8E%E1%85%A6)%20dd2c9aec237049349dd8f4be5fb47628/Untitled%206.png)
> 
> ```jsx
> f1(n) {
> 	this.name = n;
> }
> 
> f2(n,k,e,m) {
> 	f1.call(this,n);
> ...
> }
> ```
> 
> - 일반 함수 호출 방법으로는 f2() 가 this라는 변수에 받아 둔 객체 주소를 f1()에 전달할 방법이 없다.
> 
> > 생성자를 체인으로 연결하듯이 super-sub  로 만드는 이유?
> > 
> > 1. 생성자 재사용 가능
> > 2. 기능 확장이 용이
> 
> > cf. 함수를 호출하는 방법
> > 
> > 1. 함수명(아규먼트, …);
> >     
> >     eg.f1();
> >     
> > 2. 함수명.call(객체주소, 아규먼트, …); 
> >     
> >     eg. f1.call();
> >     

11-6

> **슈퍼 생성자의 prototype 사용하기**
> 
> 1. 현재 객체에서  함수 찾기
> 2. 생성자의 prototype에서 찾기
> 3. 상위생성자의 prototype에서 찾기

11-7 ~ 9

**슈퍼 생성자의 prototype 연결하기**

```jsx
// 옛날버전

// 신규 버전
// Car.prototype을 상위 생성자인 Engine.prototype과 연결한다.
Object.setPrototypeOf(하위생성자프로토타입, 상위생성자프로토타입);

Object.setPrototypeOf(Car.prototype, Engine.prototype);
```

11-10

### typeof, instanceof

- instanceof

객체를 초기화시키는데 참여한 생성자인지 검사한다.

```jsx
// 생성자 정의
function Engine(valve,cylinder,cc) {
  // Object.call(this);
  this.valve = valve; 
  this.cylinder = cylinder; 
  this.cc = cc; // cc
}
function Car(valve, cylinder, cc, capacity, auto) {
  Engine.call(this, valve, cylinder, cc); 

  this.light = false;
  this.capacity = capacity;
  this.auto = auto;
}
Object.setPrototypeOf(Car.prototype, Engine.prototype);

// Car 객체 생성
let obj = new Object();
let engine = new Engine(16, 4, 2000);
let car = new Car(16, 4, 2000, 5, true);

// typeof 연산자
console.log(typeof obj);
console.log(typeof engine);
console.log(typeof car);
console.log("-----------------------");

// instanceof 연산자
// => 객체를 초기화시키는데 참여한 생성자인지 검사한다.
console.log(obj instanceof Object);
console.log(obj instanceof Engine);
console.log(obj instanceof Car);
console.log("-----------------------");

console.log(engine instanceof Object);
console.log(engine instanceof Engine);
console.log(engine instanceof Car);
console.log("-----------------------");

console.log(car instanceof Object);
console.log(car instanceof Engine);
console.log(car instanceof Car);
console.log("-----------------------");
```