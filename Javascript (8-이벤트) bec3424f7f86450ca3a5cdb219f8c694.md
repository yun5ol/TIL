# Javascript (8-이벤트)

교재: Do it! 웹표준의정석
작업중: Done
태그: Dev, 웹&모바일, 웹프로그래밍기초
학습일: 12/14/2022

## 이벤트

### 리스너 등록하기

- 이벤트
- 리스너 = 이벤트 핸들러
    - click 이벤트
        - click 이벤트에 대해 리스너 등록하는 방법
            - **inline 방식**
            
            인라인 방식은 유지보수가 어렵다. > HTML과 JS는 분리하자. 
            
            - HTML 태그의 onclick 속성에 자바스크립트 코드를 넣는다.
                
                ```jsx
                // 이벤트를 이벤트 대상의 태그 속성으로 지정
                
                <button id="btn1-1" onclick="var str='Hello'; window.alert(str);">버튼1-1</button><br>
                
                // 더블쿼테이션 안에 문자열은 싱글쿼테이션
                
                // script탭에서 함수 생성, 태그에 지정
                
                <input id="input1" type="text1">
                <button id="btn1-2" onclick="btn1Click();">버튼1-2</button><br>
                
                ...
                
                function btn1Click() {
                  var msg = document.getElementById('input1'); 
                  if (msg.value == 'ok') {console.log('하하하'); 
                  } else {console.log('-.-');}
                };
                ```
                
            - 태그 객체의 onclick 프로퍼티에 함수를 등록한다.
            
            메소드에 담아놓고 호출될 함수를 태그에 넣어줘라
            
            하나의 이벤트만 가능
            
            ```jsx
            <button id="btn2">버튼2</button><br>
            ...
            /*
            function f1() {
                var str = "Hello2a!";
                window.alert(str);
                console.log(this); // this는 이 함수가 소속된 객체를 통해 호출될 때 그 객체를 가리킨다.
            } 
            btn2.onclick = f1; // 함수의 주소를 객체 프로퍼티로 저장하는 순간 그 객체에 소속된다.
            */
            
            /*
            // 위 보다 익명함수로 바로 선언하자.
            btn2.onclick = function() {
                var str = "Hello2b!";
                window.alert(str);
                console.log(this); // 일반 함수에서 this는 그 함수가 소속된 객체이다.
            };
            */
            
            // 위에서 arrow 함수로 한번 더
            btn2.onclick = () => {
              var str = "Hello2c!";
              window.alert(str);
              console.log(this); // arrow function에서 this는 window 객체이다.
            };
            ```
            
            - **property 방식**
                - 태그 객체의 addEventListner() 를 이용하여 호출 될 함수를 등록한다.
                    
                    ```jsx
                    var btn3 = document.querySelector("#btn3");
                    
                    btn3.addEventListener("click", btn3Click);
                    function btn3Click() { // 클릭 이벤트의 이름은 "onclick"(속성명)이 아니라, "click"이다.
                      var str = "Hi1!!";
                      window.alert(str);
                      console.log(this); // this는 btn3 객체이다.
                    }
                    
                    // 바로 익명함수 추가
                    btn3.addEventListener("click", function() {
                      var str = "Hi2!!";
                      window.alert(str);
                      console.log(this); // this는 btn3 객체이다.
                    });
                    
                    // arrow 
                    btn3.addEventListener("click", () => {
                      var str = "Hi3!!";
                      window.alert(str);
                      console.log(this); // this는 window 객체이다.
                    });
                    ```
                    
        - 3가지 리스너의 호출 순서
            - 태그의 onclick 속성 → 프로퍼티의 onclick
            - addEventListener → 프로퍼티의 onclick
                - 일관된 리스너를 이용해라
        - **각 태그 객체에 따로따로 이벤트 리스너를 등록해야 한다.**
            
            **querySelectorAll()**의 리턴 값은 **NodeList** 이다. 태그가 아니라.
            
            **따라서 addEventListener() 함수가 없다.**
            
            ```jsx
            /*
            el.addEventListener("click", () => {
                console.log(this);
            });
            */
            
            // 또한 onclick 프로퍼티도 없다.
            // 따라서 다음 코드는 의미 없다.
            /*
            el.onclick = () => {
                console.log(this);
            };
            */
            
            // 다음과 같이 각 태그 객체에 리스너를 추가하던가!
            
            for (var e of el) {
            	e.onclick = function() {
            		console.log(this);
            	}
            }
            
            // 다음처럼 한 개의 함수를 정의한 후에
            // 각 태그에 리스너로 등록하던가! "권장"
            
            function f1() {
            	console.log(this);
            }
            for (var e of el) {
            	  e.onclick = f1
            }
            
            // $는 제이쿼리 > 추후에
            //$(".btn1").on('click', function() {
            //  console.log(this);
            //});
            
            //$(".btn1").click(function() {
            //  console.log(this);
            //});
            ```
            
        
        ### 이벤트 정보 다루기
        
        이벤트가 발생하면, 웹브라우저는 이벤트 정보를 객체에 담아서 리스터를 호출할 때 파라미터로 전달한다.
        
        이벤트 객체는 이벤트 종류에 따라 **미리 정의된 생성자**에 의해서 초기화된다.
        
        **즉 이벤트 종류에 따라 특정 생성자가 이벤트 객체를 준비한다.**
        
        태그의 onclick 속성에 자바스크립트 코드를 둘 때 이벤트 정보를 사용하는 방법?
        
        **"event"** 라는 이름으로 정의된 객체가 있다. 그 객체를 사용하면 된다.
        
        ```jsx
        <button id="btn1" onclick="console.log(event)">버튼1</button><br>
        
        // => 이 event 객체는 MouseEvent()가 초기화시킨 객체이다.
        // => 즉 MouseEvent() 생성자가 추가한 속성을 사용할 수 있다.
        //
        // MouseEvent 주요 속성
        // => altKey : Alt 키 누름 여부
        // => ctrlKey : Ctrl 키 누름 여부
        // => button : 누른 버튼 번호
        // => offsetX/Y : 버튼 영역을 기준으로 X/Y 좌표
        // => clientX/Y : 웹브라우저 내용창을 기준으로 X/Y 좌표
        // => screenX/Y : 바탕화면 영역을 기준으로 X/Y 좌표
        //
        ```
        
        <aside>
        💡 pointerEvent : 손 터치의 햅틱, 탭틱 고려하여 추가됨
        
        따라서 mouseEvent를 상속함
        
        ![Untitled](Javascript%20(8-%E1%84%8B%E1%85%B5%E1%84%87%E1%85%A6%E1%86%AB%E1%84%90%E1%85%B3)%20bec3424f7f86450ca3a5cdb219f8c694/Untitled.png)
        
        </aside>
        
        ```jsx
        **// HTML 태그의 onclick 속성에 많은 자바스크립트 코드를 넣을 수 없을 때,
        // 함수를 만들고 호출하라!**
        // => 물론 event 객체를 함수를 호출할 때 넘겨줘야 한다.
        //    당연히 함수에서는 event 객체를 받는 파라미터가 있어야 한다.
        function btn1Click(e) {
          console.log(e);
          console.log(e.constructor.name);
          console.log(e instanceof MouseEvent); // 생성자 초기화에 관여했는지
        	console.log(
        			e.altKey, e.ctrlKey, e.button,
        			e.offsetX, e.offsetY,
        			e.clientX, e.clientY,
        			e.screenX, e.screenY)
        }
        
        **// 태그 객체의 onclick 프로퍼티에 리스너 등록하고 이벤트 정보 추출**
        document.getElementById("btn1").onclick = function(e) { // 변수명 맘대로 파라미터명
        	console.log(
        			e.altKey, e.ctrlKey, e.button,
        			e.offsetX, e.offsetY,
        			e.clientX, e.clientY,
        			e.screenX, e.screenY)
        };
        
        // 이런거 기대하지 말라고! 현역은 위와 같이
        /*
        var btn1 = document.getElementById("btn1");
        
        btn1.onclick("click", function(e) {...}
        */
        
        **// addEventListener() 사용**
        document.getElementById("btn1").addEventListener("click", function(e) {
        	console.log(
        		e.altKey, e.ctrlKey, e.button,
        		e.offsetX, e.offsetY,
        		e.clientX, e.clientY,
        		e.screenX, e.screenY)
        });
        // 이벤트 객체를 받고 싶으면, 파라미터 변수를 선언해라
        ```
        
        ### 이벤트가 발생된 태그 알아내기
        
        ```jsx
        <body>
        <h1>이벤트 - 이벤트가 발생된 태그 알아내기</h1>
        <button id="btn1" data-no="100">버튼1</button><br> 
        
        <script>
        "use strict"
        
        // 리스너가 일반 함수나 익명 함수일 경우,
        // this가 가리키는 객체가 이벤트가 발생된 객체이다.
        //
        document.getElementById("btn1").addEventListener("click", function(e) { 
        	console.log(this); 
        
        	// 이벤트가 발생한 객체의 속성 값 알아내기
        	// => 개발자가 임의로 추가한 속성인 경우 반드시 getAttribute()를 사용해야 한다.
        	console.log(this.getAttribute("data-no"));
        	
        	// 개발자가 태그에 임의로 추가한 속성은 다음과 같이 일반적인 방법으로 꺼낼 수 없다. 
        	console.log(this["data-no"]); // undefined
        	// data-no 속성값
        	
        	// 태그에 원래 있던 속성이라면 일반적인 문법으로 접근할 수 있다.
        	console.log(this.id);
        });
        </script>
        </body>
        
        <button id="btn1" data-no="100">버튼1</button><br>
        
        <script>
        "use strict"
        
        // arrow function인 경우
        // this는 window 객체를 가리킨다.
        //
        document.getElementById("btn1").addEventListener("click", (e) => {
          console.log(this); // window 객체이다.
        
          // 그럼 arrow function(자바에서는 Lambda라 부른다)에서는
          // 이벤트가 발생된 객체를 알 수 없는가?
          // => 있다!
          //    이벤트 객체에 이벤트가 발생된 태그의 주소가 들어 있다.
          console.log(e.target);
        
          // 이벤트가 발생한 객체의 속성 값 알아내기
          console.log(e.target.getAttribute("data-no"));
        });
        </script>
        ```
        
        ### 이벤트 단계
        
         이벤트 발생 > capture phase > target phase > bubble phase 이벤트가 발생하면 다음 3단계로 전달 된다.
         1) capture phase    
            => 부모 태그에서 자식 태그로 내려가는 단계
        2) target phase
            => 이벤트가 발생된 목적지에 도달한 단계
        3) bubble phase
            => 다시 목적지에서 부모 태그로 올라가는 단계
        
        ![Untitled](Javascript%20(8-%E1%84%8B%E1%85%B5%E1%84%87%E1%85%A6%E1%86%AB%E1%84%90%E1%85%B3)%20bec3424f7f86450ca3a5cdb219f8c694/Untitled%201.png)
        
        <이벤트 단계와 리스너 호출>
        
        ![Untitled](Javascript%20(8-%E1%84%8B%E1%85%B5%E1%84%87%E1%85%A6%E1%86%AB%E1%84%90%E1%85%B3)%20bec3424f7f86450ca3a5cdb219f8c694/Untitled%202.png)
        
        ### 이벤트 전파 막기
        
        **Event.stopPropagation()**
        
        bubbling  을 막는다.
        
        **Event.stopImmediatePropagation()**
        
        target에 등록된 함수라도 즉시 현 함수에서 실행을 마감한다.
        
        **e.target**
        
        **e.currentTarget**
        
        <aside>
        💡 클릭시 리턴 값 받지 않게
        
        ```jsx
        <td><a href="https://www.daum.net" onclick="return false;">제목입니다.</a></td>
        ```
        
        </aside>
        
        <aside>
        💡 다른 링크로 이동
        
        ```jsx
        window.location.href = "https://www.daum.net/board?no=" + e.currentTarget.getAttribute("data-no");
        ```
        
        </aside>
        
        ### 프로그래밍으로 이벤트 발생시키기
        
        > 객체와 인스턴스
        > 
        > 
        > **인스턴스 : 함수(생성자)를 통해서 초기화된 객체**
        > 
        > ![Untitled](Javascript%20(8-%E1%84%8B%E1%85%B5%E1%84%87%E1%85%A6%E1%86%AB%E1%84%90%E1%85%B3)%20bec3424f7f86450ca3a5cdb219f8c694/Untitled%203.png)
        > 
        
        **dispatchEvent()**
        
        ```jsx
        // 사용자의 행위가 아닌 프로그래밍으로 특정 이벤트를 발생시킬 수 있다.
        //
        //
        document.getElementById("btn1").addEventListener("click", function(e) {
        	// #btn1을 눌렀을 때 #btn2에 click 이벤트 발생시키기
        	// 1) MouseEvent 만들기
        	var myEvent = new MouseEvent("click"); 
        
        	// 2) 위에서 생성한 이벤트 객체를 #btn2에 보낸다.
        	document.getElementById("btn2").dispatchEvent(myEvent);
        });
        
        document.getElementById("btn2").addEventListener("click", function(e) {
            console.log("버튼2...");
        });
        ```
        
        ### 커스텀 이벤트 발생시키기 (고급)
        
        **Event()** 생성자를 사용해서 이벤트 객체를 만들어야 한다.
        
        ```jsx
        "use strict"
        
        // javascript에 정의된 이벤트가 아닌 개발자가 임의의 이벤트를 만들어 발생시킬 수 있다.
        // => Event() 생성자를 사용해서 이벤트 객체를 만들어야 한다.
        //
        document.getElementById("btn1").addEventListener("click", function(e) {
          // #btn1을 눌렀을 때 #btn2에 "ohora" 이벤트를 발생시키기
        	// 1) Event 만들기 //빌트인 생성자
        	var myEvent = new Event("ohora"); //> 이벤트를 만들었고
        
        	// 2) 위에서 생성한 이벤트 객체를 #btn2에 보낸다.
        	document.getElementById("btn2").dispatchEvent(myEvent); //> 해당 이벤트를 버튼투에 디스패치
        });
        
        // "ohora" 이벤트를 처리하고 싶다면,
        // 다음과 같이 이벤트 이름을 "ohora"로 지정하라!
        document.getElementById("btn2").addEventListener("ohora", function(e) {
          console.log("버튼2...");
        });
        ```
        
        ### **커스텀 이벤트에 데이터를 첨부해서 보내기**
        
        **CustomEvent()** 생성자를 사용해서 이벤트 객체를 만들어야 한다.
        
        ```jsx
        // 커스텀 이벤트에 데이터를 첨부해서 보내기
        // => CustomEvent() 생성자를 사용해서 이벤트 객체를 만들어야 한다.
        //
        document.getElementById("btn1").addEventListener("click", function(e) {
        	// #btn1을 눌렀을 때 #btn2에 "ohora" 이벤트를 발생시키기
        	// 1) CustomEvent 만들기
        	// => 이벤트 객체에 데이터를 첨부할 때는 "detail"이라는 이름으로 데이터를 첨부하라!
          var myEvent = new CustomEvent("ohora", {
            detail: "hello!!"
          });
        
        	// 2) 위에서 생성한 이벤트 객체를 #btn2에 보낸다.
        	document.getElementById("btn2").dispatchEvent(myEvent);
        });
        
        // "ohora" 이벤트를 처리하고 싶다면,
        // 다음과 같이 이벤트 이름을 "ohora"로 지정하라!
        document.getElementById("btn2").addEventListener("ohora", function(e) {
            console.log("버튼2...", e.detail);
        });
        
        cf.
        var data = new Object();
          data.detail = "Hello!!"
          var myEvent = new CustomEvent("ohora",data);
        
        // =
          var data = {
            detail: "Hello!!"
          }; var myEvent = new CustomEvent("ohora",data);
        
        // =
        var myEvent = new CustomEvent("ohora", {
            detail: "Hello!!"
        });
        ```
        
        ### **커스텀 이벤트에 여러 개의 데이터를 첨부해서 보내기**
        
        **CustomEvent()** 생성자를 사용해서 이벤트 객체를 만들어야 한다.
        
        ### **a 태그의 기본 동작을 중단시키기**
        
        **e.preventDefault();** (권장 # 6-1)
        
        a 태그의 기본 동작을 비활성화시킨다. 리스너 호출이 끝난 후 서버에 요청하지 않는다.
        
        ```jsx
        return false; // addEventListener()로 함수를 등록하면
                      // return 값으로 a 태그의 기본 동작을 취소할 수 없다.
        ```
        
        ### 폼
        
        - 폼의 submit 버튼 만들기
        
        ```jsx
        <form action="https://www.daum.net">
          <input type="text" name="title">
          <button>전송1</button> <!--타입 지정 없으면 디폴트는 submit-->
        </form>
        
        <form action="https://www.daum.net">
          <input type="text" name="title">
          <button type="submit">전송2</button>
        </form>
        
        <form action="https://www.daum.net">
          <input type="text" name="title">
          <input type="submit" value="전송3">
        </form>
        ```
        
        - **f**orm의 submit 동작을 중단시키기
        
        ```jsx
        <form action="https://www.daum.net" onsubmit="return false">
          <input type="text" name="title">
          <button>전송 막기1</button>
        </form>
        
        <form action="https://www.daum.net" id="form2">
          <input type="text" name="title">
          <button>전송 막기2</button>
        </form>
        
        <form action="https://www.daum.net" id="form6">
          <input type="text" name="title">
          <!-- 일반 버튼은 서버에 전송을 수행하지 않는다. -->
          <button type="button">전송 막기6</button> // # 6-3 참고
          <input type="button" value="전송 막기6">
        </form>
        
        ...
        
        <script> 
        // submit 이벤트가 발생했을 때 호출할 리스너를 등록한다.
        // submit 이벤트는 언제 발생하는가?
        // submit 버튼을 클릭할 때 발생한다.
        document.querySelector("#form2").onsubmit = () => {
          return false;
        };
        
        document.querySelector("#form3").onsubmit = (e) => {
          e.preventDefault();
        };
        
        document.querySelector("#form4").addEventListener("submit", (e) => {
          e.preventDefault();
        });
        
        document.querySelector("#form5").addEventListener("submit", (e) => {
          return false; 
        	// addEventListener()로 이벤트 핸들러를 등록할 때는
          // return false 가 의미없다. 동작되지 않는다.
          // 반드시 e.preventDefault()를 호출하라!
        });
        
        </script>
        ```