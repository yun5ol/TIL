# Javascript (3)


📓 교재: Do it! 웹표준의정석
🏷 태그: Dev, 웹&모바일, 웹프로그래밍기초
📆 학습일: 12/07/2022

### 배열

const arr = [ “aaa”, “bbb”, true, 100 ];   배열도 객체다

1. new 라는 명령어를 통해 객체 생성 ( 단축 명령어로 생략가능)
    1. const arr = new Array( ); 
        
        생성자 (constructor) : 빈 객체에 용도에 따라서 필요한 변수나 함수 등을 채워넣는 일을 하는 아주 특별한 함수 = 객체가 자신의 역할을 제대로 수행할 수 있도록 필요한 값과 함수를 준비하는 일을 한다.
        
    2. Array 호출
        
        ⬇
        
        object 생성자 호출
        
        ⬇
        
        Array( ) 실행
        
    
    c.   arr[0] = “aaa”;
    
    arr[1] = “bbb”;
    
    arr[2] = true;
    
    arr[3] = 100;
    

### for 반복문

```jsx

for(변수선언및초기화; 조건; 변수값 증가) {
 ....
}

# 19-1 
<h1>반복문 - for(;;)</h1>

"use strict"
// 인덱스를 가지고 반복할 때 사용한다.

const arr = ["aaa", "bbb", true, 100];
let i;
for (i = 0; i < arr.length; i++) { // .length 배열크기, '항상' 배열은 0부터 시작하고 배열보다 < 적게 설정
	console.log(arr[i]); // 할당문(eg a=++i) 이 아니니깐 i++이나 ++i 나 같다.
}
console.log("---------------------");

for (let x = 0; x < arr.length; x++) {  // for 문이 끝나고 x값을 알 필요가 없다면, 로컬변수로 이용하라.
    console.log(arr[x]);
}
console.log("---------------------");

console.log(i);
console.log(x); // x는 for 문에서 선언한 로컬 변수이다. 즉 for 문을 종료하면 자동으로 제거된다.

# 19-2
<h1>반복문 - for(... in 배열)</h1>

"use strict"
// 배열을 처음부터 끝까지 반복할 때 유용하다.

const arr = ["aaa", "bbb", true, 100];
let i;
for (i in arr) { // i 변수에 저장되는 것은 배열의 "인덱스"이다.
	console.log(i, arr[i]); // arr[i] "인덱스"
}
console.log("---------------------");

for (let x in arr) {
    console.log(x, arr[x]);
}
console.log("---------------------");

console.log(i);
console.log(x); // 로컬변수 fot문에서 x값 끝

```

### property 와 객체

**property** : 객체에 저장되는 값 (**숫자, 문자열, 논리, 함수주소, 객체주소 …** )

> 
> 
> 
> ```jsx
> # 19-3
> <h1>반복문 - for(... in 객체)</h1>
> const obj = new Object(); 
> 
> obj.name = "홍길동";
> obj.age = 20;
> obj.company = new Object(); // 주소 500번
> obj.company.name = "비트캠프"; // 주소 700번
> ```
> 
> 
> 함수도 객체 : 일반 객체와 다른 점은 ‘함수 코드’ 가 들어있다.
> 
> 🔸→ 다이아 + 화살표 UML (unified modeling language : 통합모델링언어
> 
>   : 단일화/통일된, 생각한 바를 글과 그림으로 표현, 글/그림을 작성하는 문법)  
> 
> eg. 알고리즘 다이어그램
> 

```jsx
# 19-4
<h1>반복문 - for(변수 선언 of 배열)</h1>
<script>
"use strict"
// 배열을 처음부터 끝까지 반복하여 값을 꺼낼 때 유용하다.

const arr = ["aaa", "bbb", true, 100];
let v;
for (v of arr) {
  // v 변수에는 인덱스가 아니라 배열에서 꺼낸 값이 저장된다. 'for(of)'
	console.log(v);
}
console.log("---------------------");

for (let x of arr) {
    console.log(x);
}
console.log("---------------------");

console.log(v);
console.log(x);
</script>

# 19-5
<h1>반복문 - for(변수 선언 of iterable 객체)</h1>
// 일반 객체는 이 반복문을 사용할 수 없다.
// iterable 프로토콜을 구현한 객체라면 이 반복문을 사용할 수 있다.
// 예) Array, Map

// 일반 객체는 for...of 반복문을 사용할 수 없다.
//실행 오류 발생!

for (var v of obj) { 
	console.log(v);
}

var obj2 = new Map(); // Map으로 초기화시킨 객체는 iterable 객체이다.
obj2.set("name", "홍길동"); // Map의 set이라는 함수가 이름 & 값을 저장
obj2.set("age", 20);
obj2.set("tel", "1111-1111");
obj2.set("working", true);

for (var x of obj2) { // map 객체는 for(of) 를 쓸 수 있다.
  // x는 배열이다.
  // x[0]은 key, x[1]은 value가 들어 있다.
  console.log(x); // eg. ["name","홍길동"]
  console.log(x[0], "=", x[1]);
}
console.log("-----------------")
```

> **배열과 destructuring “구조분해할당”**
> 
> 
> ```jsx
> 
> // destructuring 문법을 사용하여 key와 value를 분해하여 받는다.
> for (var [key, value] of obj2) {
>     console.log(key, "=", value);
> }
> 
> 19-5의 위 코드를 destructuring 을 해라
> 배열의 값이 분해되어 각각의 변수에 저장된다! : **구조분해할당**
> 
> let [key, value] = ["name", '홍길동"];
> 
> # 20-1
> <h1>구조 분해(destructuring) - 배열</h1>
> ```
> 

```jsx
# 19-6,7 건너뛰기~~~
<h1>반복문 - for(변수 선언 of iterable 객체)</h1>

# 20-1
<h1>구조 분해(destructuring) - 배열</h1>

// 값을 분해하여 여러 변수에 받을 수 있다.
//
let arr = ["홍길동", "1111-2222", true, 20];
console.log(arr);

// 보통 한 개의 변수에 한 개의 값을 받는다. ****
var n = arr[0];
var t = arr[1];
var w = arr[2]; 
var a = arr[3];
console.log(n, t, w, a);
console.log("----------------");

// 배열의 값을 분해해서 받을 수 있다. **// 순서대로! 할당 받는다**
let [name, tel, working, age] = arr;
console.log(name, tel, working, age);
console.log("----------------");

// 배열 개수 보다 적은 변수를 선언하면 그 변수 개수만큼만 분해해서 받는다.
let [name2, tel2] = arr;
console.log(name2, tel2);

# 20-2
<h1>구조 분해(destructuring) - 객체</h1>

let obj = new Object();
obj.name = "홍길동";
obj.age = 20;
obj.tel = "1111-1111";
obj.working = true;

// 객체에서 값을 여러 변수에 분리하여 담을 때는 
// 객체의 프로퍼티 이름과 같은 이름으로 변수를 선언한다.
**// => 분해 변수의 이름과 일치하는 프로퍼티 값을 넣어준다.**
var {tel, name, age, gender} = obj; // 객체 분해는 중괄호!
console.log(name);
console.log(age);
console.log(tel);
console.log(gender); // 객체에 지정된 이름의 프로퍼티가 없다면 **undefined** 이다.

// 객체에서 추출하고 싶은 프로퍼티만 추출할 수 있다.
var {name, age} = obj; // 순서하고 상관 없이 이름으로!
console.log(name, age);

# 20-3
<h1>구조 분해(destructuring) - 객체 II</h1>

var obj = new Object();
obj.name = "홍길동";
obj.age = 20;
obj.tel = "1111-1111";
obj.working = true;

// 객체에서 특정 프로퍼티 값을 분리하여 받은 후에
// 나머지 값을 별도의 객체에 담아서 받고 싶다면
// {변수1, 변수2, ...나머지값받을변수}, 객체는 중괄호!
var {age, tel, ...other} = obj; // other에 주소가 들어간다 : 나머지를 객체로 받는다.
console.log(age);
console.log(tel);
console.log(other);
console.log(other.name);
console.log(other.working);

```

> 
> 
> 
> 
> 
> ```jsx
> # 20-4
> <h1>구조 분해(destructuring) - 함수 **리턴** 값</h1>
> //배열이나 객체나 함수는 주고 받을 수 없다. 
> //말은 객체를 리턴한다. 뜻은 객체의 주소를 리턴한다.
> //각 주소를 주고 받을 뿐.
> //eg. 휴대폰에 친구저장 !== 실제 친구 저장
> 
> function f1() {
>   return ["홍길동", 100, 90, 80, 270, 90]; // 이 함수는 배열을 return한다.
> }
> 
> var r1 = f1(); // 위의 함수를 r1변수가 받는다. : 배열 자체가 아니라, 배열의 **'주소'**를 받는다
> console.log(r1);
> 
> console.log(r1[0],r1[1],r1[2],r1[3]); // 예전같으면 배열의 주소를 이렇게 불렀을 텐데!
> // r1 이라는 배열로 찾아가서 0항목, 1항목 ... 찾아온다 라는 뜻!
> 
> // 함수의 리턴 값이 배열이기 때문에
> // 배열을 값을 destructuring 하는 문법은 같다.
> var [name, kor, eng, math] = f1();
> console.log(name, kor, eng, math);
> console.log("-----------------------");
> 
> // 배열의 중간 값을 건너 뛰고 변수에 받을 수 있다.
> // 뛰어넘는 순서 만큼 , 넣을 것
> var [name,,,,sum,aver] = f1();
> console.log(name, sum, aver);
> ```
> 

```jsx
# 20-5
<h1>구조 분해(destructuring) - 함수 리턴 값 II</h1>

"use strict"

function f2() {
  var obj = new Object(); 
  obj.name = "홍길동"; 
  obj.age = 20;
  obj.tel = "1111-1111";
  obj.working = true;
  return obj;
} 

// 보통 다음과 같이 함수가 리턴한 객체를 통째로 받는다.
// 실제 객체 주소를 받는다.
var r2 = f2();
console.log(r2);
console.log("------------------------");

// 리턴 받은 객체에서 값을 꺼낼 때 
// 프로퍼티와 일치하는 이름의 변수를 선언하면 된다.
var {tel, age} = f2(); // 중괄호인 경우는 함수가 리턴하는게 '객체'구나~~ 
console.log(tel, age);
```

### 변수

```jsx
# 21-1

<h1>변수 - const</h1>

// var 로 선언한 변수는 값을 변경할 수 있다.
var v1 = 100;
v1 = 200;
console.log(v1);

// const로 선언한 변수는 값을 변경할 수 없다.
const v2 = 100;
//v2 = 200; // 주석 풀면 에러 발생
console.log(v2);

// const 변수는 선언할 때 값을 할당해야 한다.
//const v3; // 예외 발생!
//v3 = 100;
//console.log(v3);
console.log("---------------------------");

const v4 = "오호라";
console.log(v4);
console.log(window.v4); // const 변수는 window 객체에 보관되지 않는다.

# 21-2
<h1>변수 - const 객체</h1>

// const 변수에 객체를 할당한다면,
// => 실제로 객체의 주소가 할당되는 것이다.
// 변수를 다른 객체의 주소로 변경할 수 없지만,
// => 그 변수가 가리키는 객체에 대해서는 변경할 수 있다.
// 즉 const 로 선언한 변수는 변수의 값만 못 바꾼다는 것이다.
const v2 = new Object();
v2.name = "홍길동";
v2.age = 20;
v2.tel = "1111-2222";
console.log(v2);

// const 변수의 값은 변경할 수 없다.
//v2 = new Object(); // 주석 풀면 예외 발생!

// 그러나 const 변수가 가리키는 객체의 프로퍼티는 바꿀 수 있다.
v2.name = "임꺽정";
v2.working = true;
console.log(v2);

# 22-1
<h1>변수 - let</h1>

var v1 = "홍길동";
{
  var v1 = "임꺽정"; // 기존 변수의 값을 변경한다.
  var v2 = 20; // 새 글로벌 변수를 추가한다. 
}
console.log(v1, v2);
console.log("--------------------");

var v3 = "홍길동";
{
  // let으로 선언한 변수는 사용 범위가 블록으로 한정(block-scoped)된다.
  let v3 = "임꺽정"; // 새 로컬 변수이다. 글로벌 변수가 아니다.
  let v4 = 30; // 새 로컬 변수이다. 글로벌 변수가 아니다.
  console.log(v3, v4);
  
}
console.log(v3); // OK
//console.log(v4); // let으로 선언한 변수는 그 블록을 벗어나면 사용할 수 없다.
console.log("--------------------");

let v4 = "오호라";

console.log(v4); 
console.log(window.v4); // let(또는 const) 으로 선언한 변수는 window 객체에 보관되지 않는다.

# 22-2
<h1>변수 - let II</h1>

// if, for 등의 블록에서 var로 선언한 변수는 글로벌 변수이다.
for (var i = 0; i < 5; i++) {
  console.log(i);
}
console.log("==>", i);
console.log("==>", window.i); // 글로벌변수는 window 객체에 저장돼!
console.log("--------------------")

for (let x = 0; x < 5; x++) {
  console.log(x);
}
// for 블록 안에서 let으로 선언한 변수는
// for 블록을 벗어나면 자동으로 제거되기 때문에 사용할 수 없다.
console.log("==>", x);
```
