# Javascript (2)

교재: Do it! 웹표준의정석
작업중: In progress
태그: Dev, 웹&모바일, 웹프로그래밍기초
학습일: 12/06/2022

javascript > ex01

```bash
# 11-4
//상수는 한 번 값을 저장하면 바꿀 수 없다.
// obj = new Object(); 예외발생

//그러나 상수가 가리키는 객체를 바꾸는 것은 상관없다.
//왜? obj라는 상수에 저장된 주소가 바뀌는 것은 아니기 때문이다.

# ex02 -> exam18-2

* 문법
Literal > 값을 표현하는 문법
eg. "aaa", 'aaa'... 프로그램 언어마다 표현하는 방식이 다르다.

Variables > 값을 저장하는 문법
eg. var/let/const/[]

if~else/switch 분기문 > 명령문의 실행 흐름을 제어
while/for 반복문도 마찬가지  : 다 묶어서 제어문

function > 명령을 재사용할 수 있도록/관리하기 쉽도록 기능단위로 묶는 문법

object > 데이터를 다루기 쉽도록 그룹으로 묶는 방법
				함수들을 관리하기 쉽도록 역할 단위로 그룹화하는 문법

module > 객체와 함수들을 재사용하기 쉽도록 그룹으로 묶는 문법
```

```jsx
# 17-1
할당 연산자는 오른쪽의 연산자가 모두 수행되면 최종으로 마지막에 할당연산자가 수행된다.

		console.log(100 + 200);
		console.log(100 - 200);
		console.log(100 * 200);
		console.log(100 / 200);
		console.log(100 % 200);
		console.log(2 ** 4); // 2의 4제곱 '16'
		console.log("---------------");		

		y = 100;
		y = y++;
		// temp = y;
		// y = y + 1;
		// y = temp;
		console.log(y); // 100

		x = 100;
		x = ++x;
		console.log(x); // 101

		a = 100 ;
		x = a++ + a++ + a++;
		// temp = a; (temp 는 임시값)
		// a = a + 1;
		// temp = temp + a;
		// a = a + 1;
		// temp = temp + a;
		// a = a + 1;
		// x = temp;
		// x = 100+101+102

		a = 3;
		x = a++ + a++ * a++;
		// 숫자 먼저 다 바꾸고(++), 사칙연산 시작 => ++, -- 연산자는 *, /, % 보다 우선한다.
		// x = 3 + 4 * 5;  
		console.log(x); // 23

# 17-3
<title>연산자 - 연결연산자</title>
</head>
<body>
<script>
"use strict"

let str1 = "Hello";
let str2 = "world";
console.log(str1 + "," + str2);

console.log(str1 + 100); //100은 문자열로 바뀐다!

console.log("100" + "200") // 100200으로 출력

console.log('----------------');
</script>
</body>

# 17-4
<title>연산자 - 비교연산자</title>
</head>
<body>
<script>
"use strict"

console.log("hello" == "hello"); //true
console.log("Hello" == "hello"); //false
console.log("----------------");

console.log("100" == 100); // true // == 연산 전에 숫자 100 문자열 "100"로 바꿔서 비교 = 형변환
console.log("100" === 100); // false // === 두 피 연산자가 같은 타입이면서 같은 값 일때, true // 즉 엄격히 비교한다. 형변환을 제한한다.
console.log("100" != 100); // false : 두 피연산자 비교 전에 형변환이일어난다.
console.log("100" !== 100); // true // 타입자체가 다르니, 따질 것 없이 다르다! true

console.log(100 < 200);
console.log(100 <= 200);
console.log(100 > 200);
console.log(100 >= 200);
console.log("----------------");

// 문자열은 문자 코드값(유니코드)으로 비교
console.log("AB" > "AC"); // false 41+42 > 41+43 
console.log("a" > "A"); // true 61 > 41
console.log("똘" < "똠"); // true  
console.log("----------------");

</script>
</body>

# 17-5
<title>연산자 - 논리연산자</title>
</head>
<body>
<script>
"use strict"
</script>
</body>

# ex02 > exam 01 를 exam 01-1 수정
# exam 01-2
<script>
"use strict";

console.log(100); // 10진수
console.log(0x64); // 16진수(기본)
console.log(0X64); // 16진수
//console.log(0144) // 0으로 시작하면, 8진수 // 공학용 계산기, 프로그래머용 <== ECMAScript 5(2009)의 strict 모드에서 8진수 표현 불가
console.log(0o144); // 8진수 사선 없는 (소문자 기본) <== ECMAScript 2015(6)에서는 0o, 0O 접두사를 붙여 8진수 표현
console.log(0O144); // 8진수
console.log(0b01100100) // 0b앞에 있으면 2진수 (소문자 기본)
console.log(0B01100100) // 0B앞에 있으면 2진수

// toString(진수) : 진수변환 함수
let a = 100;
console.log(a.toString(10)); // 100
console.log(a.toString(8)); // 144
console.log(a.toString(2)); //1100100
console.log(a.toString(16)); //64
console.log('----------------------------');
</script>

# exam 17-6
<title>연산자 - 비트연산자</title>

<script>
"use strict"

let a = 0b01100100; // 100
let b = 0b11110000; 

// AND 비트 연산자
// - 두 비트가 1일 때 1, 그 외 0
// - 1로 설정한 비트의 값은 그대로 통과하는 효과가 있다.
// - 특정 비트의 값만 추출 할 때 활용한다.
// 
console.log((a & b).toString(2)); // ==> 1100000 (맨 앞의 0은 생략된다)

// 응용1
// - 색상 값에서 빨강색 제거하기
// - eg. 사진에서 빨강색 제거하기 
// - eg. 사진 빈티지 느낌 줄 때 노란색 추가하기
let color = 0xFF00FF; //레드0xFF,블루00FF : 보라색
console.log((color & 0x00FFFF).toString(16)); //ff = 0000ff

						* 이미지와 바이트 수
							1. 흑백사진 => 1 픽셀 크기 = 1 비트 (0=검은색 1=흰색)
												=> 9 픽셀 크기 : 1 픽셀=1 비트, 9 픽셀=9 비트
							2. 칼라사진 => 각 비트값 : RGB 3 byte
												=> 9 픽셀 크기 : 27 byte
							3. HD급 크기 사진 => (1920 x 1080) x 3 = 6,220,800 byte
																	2,073,600 픽셀		= /24 = 6,075 KB
															      픽셀 = 화소			= 5.93 MB				

// OR 비트 연산자
// - 두 비트 중에 한 개라도 1이면 결과는 1, 그 외 0
// - AND 비트 연산자와 반대로 동작
// - 0 비트는 그대로 통과, 1 비트는 차단(1로 만든다.)=기존 값 제거
console.log((a | b).toString(2)); // 11110100
console.log('--------------------');

// 응용
// - 특정 색상을 강화하기
// - eg. 빨강색 강화하기
color = 0x283386;
console.log((color.toString(2)));
console.log((color | 0x550000).toString(2)); // 빨강색 강화 ; 01010101
// 기존의 빨강색 : 00101000
//  빨강색 강화: | 01010101
// --------------------
// 변경된 색상 01111101
console.log('--------------------');

// XOR(exclusive OR) 비트 연산자
// - 두 비트의 값이 다를 때 1, 같으면 0
console.log((a ^ b).toString(2));
// a: 01100100
// b: 11110000 ^
// --------------
//    10010100 
console.log('--------------------');

// NOT 비트 연산자
console.log((~a).toString(2));
// a: 01100100
// ------------
// ~  10011011 => -1100101 ???????
console.log('--------------------');

// << 비트 이동 연산자
// - 왼쪽으로 지정한 비트만큼 이동시킨다.
// - 오른쪽의 빈 자리는 0으로 채운다.
// - 1비트 이동할 대 마다 *2 한 효과가 있다.
// - *2 연산을 수행하는 것 보다 비트 이동 연산자가 실행 속도가 더 빠르다.
// - n 비트 이동 = 값 * 2**n (2의 n승 곱하기)
a = 7; // 00000111
console.log((a * 2).toString(2));  // 14
console.log((a << 1).toString(2)); // 1110 (14)
console.log((a * 4).toString(2));  // 28
console.log((a << 2).toString(2)); // 11100 (28)
console.log((a * 8).toString(2));  // 56
console.log((a << 3).toString(2)); // 111000 (56)
console.log('--------------------');

// >> 비트 이동 연산자
// - 오른쪽으로 지정한 비트만큼 이동시킨다.
// - 비어 있는 왼쪽 빈 자리는 부호비트(양수: 0, 음수:1)로 채운다.
// - 1비트 이동할 때 마다 /2 한 효과가 있다.
// - / 2 연산을 수행하는 것 보다 비트 이동 연산자가 실행 속도가 더 빠르다.
// - n 비트 이동 = 값 / 2**n (2의 n승 나누기)
a = 100; // 01100100
console.log((a / 2).toString(2));  // 50
console.log((a >> 1).toString(2)); // 0110010|0 (50)
console.log((a / 4).toString(2));  // 25
console.log((a >> 2).toString(2)); // 011001|00 (25)
console.log((a / 8).toString(2));  // 12.5
console.log((a >> 3).toString(2)); // 01100|100 (12) // overflow는 잘라버림

a = -100;             // 11111111 11111111 11111111 10011100   (-100)
console.log(a >> 1);  // 11111111 11111111 11111111 11001110|0 (-50)
//  50 : 0011 0010
// -50 : 1100 1110
console.log((a >> 1).toString(2)); 
console.log('--------------------');

// >>> 비트 이동 연산자
// - 오른쪽으로 지정한 비트만큼 이동시킨다.
// - 비어 있는 왼쪽 빈 자리는 0으로 채운다. 음수를 비트이동하면 양수로 바뀐다.
// - 양수인 경우 1비트 이동할 때 마다 /2 한 효과가 있다.
// - 양수인 경우, n 비트 이동 = 값 / 2**n (2의 n승 나누기)
a= 100;
console.log(a >>> 1)
console.log((a >>> 1).toString(2));

a = - 100;           // 11111111 11111111 11111111 10011100 (-100)
console.log(a >>> 1) // 2147483598 (양수가 됐네)
console.log((a >>> 1).toString(2)); // 01111111 11111111 11111111 11001110
console.log('--------------------');

</script>
</body>

# 17-7
연산자 - 기타연산자
<body>
  <button id = "btn1"></button> 
<script>
"use strict"

// 조건 연산자
// - 조건 ? 표현식1 : 표현식2;
// - 조건이 참이면, 표현식 1을 실행하고 그 결과를 리턴한다.
// - 조건이 거짓이면, 표현식2를 시랳ㅇ하고 그 결과를 리턴한다.
//
let age = 27;

let message = age < 20 ? "미성년입니다." : "성년입니다.";
console.log(message);
// console.log(age < 20 ? "미성년입니다." : "성년입니다."); 동일하다

// 조건 연산자를 수행한 후 결과를 반환하는 용도로 사용하라.
// 다음과 같이 결과를 반환하지 않는 문장을 실행하려면 조건문을 사용하라.
age < 20 ? console.log("미성년입니다.") : console.log("성년입니다");

if (age < 20) {
  console.log("미성년입니다.");
} else {
  console.log("성년입니다.")
}
console.log('--------------------');

// 쉼표 연산자
let a = 100, 
    b = 200, 
    c = 300;
console.log(a, b, c);
console.log('--------------------');

// 단항 연산자
const obj = new Object();
obj.name = "홍길동"; // (.name) 객체 변수 = 프로퍼티
obj.age = 20;

console.log(obj);
console.log('--------------------');

// delete 연산자
// - 객체에 추가한 프로퍼티를 제거한다.
delete obj.name;
console.log(obj);

delete obj['age']; // 객체에 추가한 프로퍼티를 제거하는게 delete 이라는 연산자
console.log(obj);
console.log('--------------------');

// typeof 연산자 
// - 피 연산자 타입을 문자열로 출력한다.
let v = "홍길동";
console.log(typeof v);

v = 100;
console.log(typeof v);

console.log((typeof v) == "number")
console.log('--------------------');

// void 연산자
// - 표현식의 결과를 리턴하지 않는다.
// - 문장 중에 실행 결과를 리턴하는 문장(statement)을 표현식(expression)이라고 한다. 

let x = 20;
let y = 30;

console.log(x + y); // x + y 문장은 표현식이다. 왜? 값을 리턴하기 때문이다.
console.log(void (x + y)); // undefined
console.log('--------------------');

// in 연산자
// - 객체에 해당 이름을 가진 프로퍼티가 있는지 검사한다.

const obj2 = {
  name: "홍길동",
  age: 20,
  working: true,
  print() {
    console.log(this.name + '(' + this.age + ',' + this.working + ')');
  }
};

console.log(obj2);
obj2.print();

console.log('name' in obj2); // in 객체 dksdp ''연산자가 있느냐
console.log('age' in obj2);
console.log('working' in obj2);
console.log('print' in obj2);
console.log('tel' in obj2);
console.log('--------------------');

// instanceof
// - 객체를 만들 때 초기화시킨 생성자가 맞는지 검사한다.
// - 초기화에 관여했다면 콘솔 로그 true
const obj3 = new Object();
const obj4 = {};
const obj5 = new Date();

console.log(obj3 instanceof Object);
console.log(obj4 instanceof Object);
console.log(obj5 instanceof Object);

const obj6 = document.getElementById("btn1");
console.log(obj6);
console.log(obj6.constructor);
console.log(obj6 instanceof HTMLButtonElement);
console.log(obj6 instanceof HTMLElement);
console.log(obj6 instanceof Element);
console.log(obj6 instanceof Node);
console.log(obj6 instanceof EventTarget);
console.log(obj6 instanceof Object);
console.log(obj6 instanceof Date);

</script>
</body>   + 그림 첨부!!
```

```jsx
# 18-2 조건문 - if...else
<script>
"use strict"

var score = 10;

if (score >= 19) {
  console.log("성년입니다.");
} else {
  console.log("미성년입니다.");
}

</script>

# 18-3 if문
var score = window.prompt("나이를 입력하세요");

if (score >= 65) // 아래 else와 한문장이라 중괄호 생략
  console.log("노인입니다.");
 else // 아래 if ~ else 가 한문장이라 중괄호 생략
  if (score >= 50) // 아래 else와 한문장이라 중괄호 생략
    console.log("장년입니다.");
   else // 아래 if ~ else 가 한문장이라 중괄호 생략
    if (score >= 35) // 아래 else와 한문장이라 중괄호 생략
      console.log("중년입니다.");
     else // 아래 if ~ else 가 한문장이라 중괄호 생략
      if (score >= 19) // 아래 else와 한문장이라 중괄호 생략
        console.log("청년입니다.");
      else // 아래 if ~ else 가 한문장이라 중괄호 생략
        if (score >= 12) // 아래 else와 한문장이라 중괄호 생략
          console.log("청소년입니다.");
        else // 아래 if ~ else 가 한문장이라 중괄호 생략
          if (score >= 7) // 아래 else와 한문장이라 중괄호 생략
            console.log("어린이입니다.");
          else 
            console.log("유아입니다."); // 문장이 한개일 땐 중괄호 생략 & if 와 else를 한 문장으로 간주
          

            
// 보기 좋게 정리해서 마치 하나의 if문으로 보이지만, 자바스크립트에 else if 문은 없다 
그리고 아래 형태를 주로 이용한다.

if (score >= 65)
  console.log("노인입니다.");
else if (score >= 50) 
  console.log("장년입니다.");
else if (score >= 35) 
  console.log("중년입니다.");
else if (score >= 19) 
  console.log("청년입니다.");
else if (score >= 12)
  console.log("청소년입니다.");
else if (score >= 7)
  console.log("어린이입니다.");
else 
  console.log("유아입니다.");

# 18-4  조건문 - switch
<script>
"use strict"

var auth = window.prompt("권한명을 입력하세요!");

if (auth == "admin")
  console.log("관리자입니다.");
else if (auth == "user")
  console.log("일반 사용자입니다.");
else if (auth == "guest")
  console.log("손님입니다.");
else 
  console.log("사용 권한이 없습니다.");

    ⬇ 서로 같다

switch (auth) {  // 맞는 case에 도달하여 log 출력 후 break
case "admin":
  console.log("관리자입니다.");
  break;  // break가 없을 경우, 아래 값 모두 출력
case "user":
  console.log("일반 사용자입니다.");
  break;
case "guest":
  console.log("손님입니다.");
  break;
default:
  console.log("사용 권한이 없습니다");
} 
</script>

# 18-5 break가 없는 경우 > 필요한 경우에 생략 > 없을 때는 위>아래로 순차 출력
var field = window.prompt("지원 분야를 입력하세요!");

switch (field) {
case "개발":
  console.log("정보처리 자격증 제출");
case "관리":
  console.log("졸업증명서 제출");
case "경비":
  console.log("이력서 제출");
  break;
default:
  console.log("지원 분야가 옳지 않습니다.");
} // 모든 값이 필요하니깐, 모두 출력됨
```