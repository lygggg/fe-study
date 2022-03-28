# 1 week

## 1. 이벤트 위임

- 이벤트 위임은 여러 개의 하위 DOM 요소에 각각 이벤트 핸들러를 등록하는 대신 하나의 상위 DOM 요소에 이벤트 핸들러를 등록하는 방법을 말한다.
- 장점
    - 각 DOM 요소에 이벤트 핸들러를 등록할 필요가 없음
    - 새로 추가된 하위 DOM 요소에도 적용 가능
- 단점
    - 원하는 DOM 요소만 실행될 수 있도록 주의
- 이벤트 전파
    - 캡쳐링 : 이벤트 객체가 window에서 시작해서 이벤트 타깃 방향으로 전파
    - 버블링 : 이벤트 객체가 이벤트 타깃에서 시작해서 window 방향으로 전파

## 2. this가 JavaScript에서 어떻게 작동하는지 설명

1. 함수를 호출할 때 `new` 키워드를 사용하는 경우, 함수 내부에 있는 `this`는 완전히 새로운 객체입니다.
2. `apply`, `call`, `bind`가 함수의 호출/생성에 사용되는 경우, 함수 내의 `this`는 인수로 전달된 객체입니다.
3. `obj.method()`와 같이 함수를 메서드로 호출하는 경우, `this`는 함수가 프로퍼티인 객체입니다.
4. 함수가 자유함수로 호출되는 경우, 즉, 위의 조건 없이 호출되는 경우 `this`는 전역 객체입니다. 브라우저에서는 `window` 객체입니다. 엄격 모드(`'use strict'`) 일 경우, `this`는 전역 객체 대신 `undefined`가 됩니다.
5. 위의 규칙 중 다수가 적용되면 더 상위 규칙이 승리하고 `this`값을 설정합니다.
6. 함수가 ES2015 화살표 함수인 경우 위의 모든 규칙을 무시하고 생성된 시점에서 주변 스코프의 `this`값을 받습니다.

## 3. 프로토타입 상속이 어떻게 작동하는지 설명

- 상속은 객체 프로그래밍의 핵심 개념으로 어떤 객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 그대로 사용할 수 있는 것
- 장점
    - 불필요한 중복 제거
    - 예) 원의 넓이 구하기 메소드 상속
    
    ```jsx
    function Circle(radius){
    	this.radius = radius;
    	this.getArea = function () {
    		return Math.PI * this.radius ** 2
    	}
    }
    
    const circle1 = new Circle(2);
    const circle2 = new Circle(3);
    console.log(circle1.getArea === circle2.getArea) // false
    ```
    
    모든 객체는 radius 프로퍼티와 getArea 메소드를 가짐
    
    Circle 생성자 함수는 getArea 메서드를 중복 생성하고 모든 인스턴스가 중복소유
    
    ```jsx
    function Circle(radius){
    	this.radius = radius;
    }
    
    Circle.prototype.getArea = function () {
    	return Math.PI * this.radius ** 2
    }
    
    const circle1 = new Circle(2);
    const circle2 = new Circle(3);
    console.log(circle1.getArea === circle2.getArea) // true
    ```
    
    getArea는 단 하나만 생성되어 프로토타입인 Circle.prototype의 메서드로 할당되어 Circle 생성자 함수가 생성하는 모든 인스턴스는 getArea 메서드를 상속받아 사용할 수 있음


## 4. AMD vs CommonJS에 대해 어떻게 생각

- 자바스크립트는 script 태그를 사용하여 외부의 자바스크립트 파일을 로드할 수는 있지만 파일마다 독립적인 파일 스코프를 갖지 않는다.
- 단점
    - 자바스크립트 파일을 여러개로 분리해도 하나의 자바스크립트 파일 내에 있는 것처럼 동작
    - 모든 자바스크립트 파일은 하나의 전역을 공유하여 중복되는 문제 발생할 수 있음
- 필요성
    - 자바스크립트를 클라이언트 사이드, 즉 브라우저 환경에 국한하지 않고 범용적으로 사용하려는 움직임이 생기면서 모듈 시스템은 반드시 해결해야하는 하는 문제
- 모듈 시스템 2가지
    - CommonJS
        - Node.js는 모듈 시스템의 사실상 표준인 CommonJS를 채택
    - AMD
        - Asynchronous Module Definition으로 비동기적 모듈 선언
        - 브라우저에서는 파일 단위의 스코프가 없다. 또한 script 태그를 사용하여 파일을 차례대로 로드한다면, 전역 변수가 겹치는 문제도 발생한다. 이러한 문제점을 해결하기 위하여 CommonJS 는 서버 모듈을 비동기적으로 클라이언트에 전송할 수 있는 `모듈 전송 포맷`을 추가로 정의했다. 서버사이드에서 사용하는 모듈을 브라우저에서 사용하는 모듈과 같이 전송 포맷으로 감싼다면 서버 모듈을 비동기적으로 로드할 수 있게 된다.
- ES6 모듈(ESM)
    - ES6에서 클라이언트 사이드 자바스크립트에서도 동작하는 모듈 기능을 추가
    ```jsx
    <script type="module" src="app.js></script>
    ```

## 5. 다음이 IIFE로 작동하지 않는 이유를 설명하세요: function foo(){ }();를 IIFE로 만들기 위해서는 무엇을 바꿔야하나요?

- IIFE는 즉시 함수 호출 표현식(Immediately Invoked Function Expressions)

# 2 week

## 6. null, undefined, undeclared의 차이점은 무엇인가요? 어떻게 이 상태들에 대한 확인을 할 것인가요?

1. null
    1. 사용자가 명시적으로 ‘없음’을 표현하기 위해 대입한 값
    
    ```jsx
    var test3; //변수 선언. 
    test3 = null; //선언한 변수 test3에 null값 할당. 
    console.log(test3); //null 
    console.log(typeof test3); //변수 test3의 타입은 object 객체
    
    ```
    
2. undefined
    1. 변수는 선언되었지만, 값이 할당되지 않은 변수
    
    ```jsx
    var test; 
    console.log(test); //undefined 
    console.log(typeof test); //undefined
    
    ```
    
3. undeclared
    1. 접근 가능한 스코프에 변수 선언조차 되어있지 않은 상태
    
    ```jsx
    console.log(test2); 
    // 오류
    /* Uncaught ReferenceError: test2 is not defined at <anonymous>:1:13 */
    
    ```

## 7. 클로저는 무엇이며, 어떻게/왜 사용하나요?

1. 외부함수 보다 내부함수가 더 오래 유지되는 경우 내부함수는 이미 생명 주기가 종료한 외부 함수의 변수를 참조할 수 있다. 이 때 내부함수를 클로저 라고 함
2. 활용
    1. 상위스코프에 대한 참조는 함수가 실행된 위치가 아니라 **함수가 정의된 위치**에 의해 결정(렉시컬 스코프)
    2. 상태가 의도치 않게 변경되지 않도록 안전하게 은닉하고 특정 함수에게만 상태 변경을 허용하여 상태를 안전하게 변경하고 유지하기 위해 사용

```jsx
const x = 1;
    
    function outerFunc(){
    	const x = 10;
    	function innerFunc(){
    		console.log(x);   // 10
    	}
    	innerFunc();
    }
    
    outerFunc();
```

```jsx
const x = 1;
    
    function outerFunc(){
    	const x = 10;
    	innerFunc();
    }

    function innerFunc(){
    	console.log(x);   // 1
    }
    
    outerFunc();
```

## 8. .forEach 루프와 .map() 루프 사이의 주요 차이점을 설명할 수 있나요? 왜 둘 중 하나를 선택할 것인가요?

1. forEach와 map
2. 공통점
    1. 배열 메소드
    2. 배열의 요소를 반복
3. 차이점
    1. forEach
        1. 값을 반환하지 않음
    2. map
        1. 함수 호출한 결과로 새 배열을 작성하여 반환

## 9. 익명 함수의 일반적인 사용 사례는 무엇인가요?

1. 의미
    1. 사용자가 함수를 만들 때 이름을 지정하지 않고 변수 혹은 그냥 호출만으로 선언할 수 있는 함수
    2. 호이스팅 되지 않음
    3. 활용
        1. 익명함수는 IIFE로 사용되어 지역 범위 내에서 일부 코드를 캡슐화하므로 선언된 변수가 전역 범위로 누출되지 않음
        
        ```jsx
        (function () {
          // 코드
        })();
        ```
        
    
    ```jsx
    SayHello(); // "hello!" 가 정상적으로 출력됨.
    
    function SayHello(){
      console.log("hello!");
    }
    
    SayHello(); // "hello!" 가 정상적으로 출력됨.
    
    // 호이스팅 된 모습
    //
    // function SayHello(){      <- 함수 선언이 먼저 일어나고,
    //   console.log("hello!");
    // }
    //
    // SayHello(); <- 첫 번째 SayHello();
    // SayHello(); <- 두 번재 SayHello();
    ```
    
    ```jsx
    //익명 함수
    
    sayHello(); // Uncaught ReferenceError: Cannot access 'sayHello' before initialization
    
    let sayHello = function() {
      console.log("hello!");
    }
    
    sayHello(); // 위에서 에러가 났으니 출력이 나오지 않음
    
    // 이 자바스크립트를 읽을 때(호이스팅 된 모습)
    // 
    // const sayHello;
    //
    // sayHello(); <- sayHello의 초기화가 진행되지 않았다.
    // 
    // sayHello = function(){
    //   console.log("hello!");
    // }
    //
    // sayHello(); <- 초기화는 진행된 후 불렸으니, 원래대로라면 출력 가능
    ```

## 10. 코드를 어떻게 구성하나요? (모듈 패턴, 고전적인 상속?)

1. Flux
    1. FLUX 패턴은 MVC의 **양방향 데이터 바인딩**의 단점을 해결하고자 페이스북에서 고안한 `단방향 데이터 바인딩` 방식의 디자인 패턴이다. 구조는 다음과 같다.
    2. 양방향 데이터 바인딩 방식은 모델의 변화에 따라 바로바로 뷰가 변하기 때문에 시스템이 복잡해질 수록 예측 불가능한 상황들이 생기고 데이터들이 꼬여버릴 수 있다는 단점

![https://taeny.dev/static/8ef687083384d183ff57c029daa5a6c4/9f82e/flux.png](https://taeny.dev/static/8ef687083384d183ff57c029daa5a6c4/9f82e/flux.png)

- **Dispatcher** : Flux의 모든 데이터 흐름을 관리하는 허브 역할을 하는 부분
- **Store** : 데이터(상태)를 저장하는 부분
- **View** : Store의 변화를 감지하고 View를 업데이트해주는 부분. Controller View라고도 부른다.

즉, “Action이 dispatch > dispatcher는 action에 맞게 store를 업데이트 > View는 store의 변화가 감지되면 view업데이트” 의 방식으로 진행된다. 대표적으로 React와 Redux가 flux패턴을 사용하며, Vuex라이브러리도 flux패턴에 영감을 받아 만들어졌다고 한다.

## 11. 호스트 객체와 내장 객체의 차이점은 무엇인가요?

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c2dcf850-9799-47e1-854e-842264ebda19/Untitled.png)

- 내장객체(Native objects or Built-in objects or Global Objects)
    - ECMAScript 명세에 정의된 객체를 말하며 애플리케이션 전역의 공통 기능을 제공
        - Object, String, Number, Function, Array, RegExp, Date, Math와 같은 객체 생성에 관계가 있는 함수 객체와 메소드로 구성
        - 네이티브 객체를 **Global Objects**
        라고 부르기도 하는데 이것은 전역 객체(Global Object)와 다른 의미로 사용되므로 혼동에 주의
        - 전역 객체(Global Object)
            - 모든 객체의 최상위 객체를 의미
            - 일반적으로 Browser-side에서는 `window`
            - Server-side(Node.js)에서는 `global`
             객체를 의미
- 호스트객체
    - 브라우저 환경에서 제공하는 window, XmlHttpRequest, HTMLElement 등의 DOM 노드 객체와 같이 호스트 환경에 정의된 객체
    - 브라우저에서 동작하는 환경의 호스트 객체
        - 전역 객체인 window, BOM(Browser Object Model)과 DOM(Document Object Model) 및 XMLHttpRequest 객체 등을 제공

## 12. function Person(){}, var person = Person(), var person = new Person()의 차이점은 무엇인가요?

- **`function Person(){}`**
    - 함수선언문
- **`var person = Person()`**
    - 
- **`var person = new Person()`**
    - 생성자 함수
    - `Person.prototype`을 상속받은 `new` 연산자를 사용하여 `Person` 객체의 인스턴스를 생성

## 13. .call과 .apply의 차이점은 무엇인가요?

# **`.call`과 `.apply`의 차이점은 무엇인가요?**

- Function 메소드
- apply
    - 호출할 함수의 인수를 배열로 묶어서 전달
    - this로 사용할 객체를 전달하면서 함수를 호출
    
    ```jsx
    const arr = [2,3,4];
    Math.min.apply(null, arr) // 2
    Math.min(a) // NaN
    Math.min(...arr) // 2
    ```
    
- call
    - 호출할 함수의 인수를 쉼표로 구분한 리스트 형식으로 전달
    - this로 사용할 객체를 전달하면서 함수를 호출
    ```jsx
    Math.min.apply(null, 2,3,4) // 2
    ```
    ```jsx
    function getThisBinding(){
    return this;
    }

    const thisArg = { a: 1};
    console.log(getThisBinding.apply(thisArg, [1,2,3])); 

    // {a:1}
    console.log(getThisBinding.apply(thisArg, 1,2,3)); 
    // {a:1}
    ```
## 14. Function.prototype.bind에 대해 설명하세요.

- apply, call 메서드와 다르게 함수를 호출하지 않고, this로 사용할 객체만 전달

```jsx
function getThisBinding(){
 return this;
}

const thisArg = { a: 1};
console.log(getThisBinding.bind(thisArg)); // getThisBinding
console.log(getThisBinding.bind(thisArg)()); // {a:1}
```
## 15. 언제 document.write()를 사용하나요?

- `document.write()`는 `document.open()`에 의해 열린 문서 스트림에 텍스트 문자열을 씁니다. 페이지가 로드된 후에 `document.write()`가 실행되면 `document.open`을 호출하여 문서 전체를 지우고 (`<head>`와 `<body>`를 지웁니다!). 문자열로 주어진 매개 변수 값으로 대체합니다. 그러므로 일반적으로 위험하고 오용되기 쉽습니다.
- `document.write()`가 코드분석이나 [JavaScript가 활성화된 경우에만 작동하는 스타일을 포함하고 싶을 때](https://www.quirksmode.org/blog/archives/2005/06/three_javascrip_1.html) 사용되는 경우를 설명하는 온라인 답변이 몇 가지 있습니다. 심지어 HTML5 보일러 플레이트에서 [스크립트를 병렬로 로드하고 실행 순서를 보존](https://github.com/paulirish/html5-boilerplate/wiki/Script-Loading-Techniques#documentwrite-script-tag)할 때도 사용됩니다! 그러나, 저는 그 이유가 시대에 뒤떨어진 것으로 생각하고 있으며, 현재는 `document.write()`를 사용하지 않고도 할 수 있습니다. 이것이 틀렸다면 고쳐주세요.

## 16. Ajax에 대해 가능한 한 자세히 설명하세요.
## 17. Ajax를 사용하는 것의 장단점은 무엇인가요?

- Ajax(asynchronous JavaScript and XML)
    - 자바스크립트를 사용하여 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 서버가 응답한 데이터를 수신하여 웹페이지를 동적으로 갱신하는 프로그래밍 방식
    - 브라우저에서 제공하는 Web API인 XMLHttpRequest 객체를 기반으로 동작
        - XMLHttpRequest
            - HTTP 비동기 통신을 위한 메서드와 프로퍼티 제공
        - JSON
            
            클라이언트와 서버간 HTTP 통신을 위한 텍스트 데이터 포맷
            
            키와 값으로 구성된 순수한 텍스트
            
            키는 반드시 큰따옴표 사용
            
            값 문자열은 반드시 큰따옴표 사용
            
            ![Ajax 생명 주기](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5479450c-f1cb-42f2-b785-64edb96f7814/Untitled.png)
            
            Ajax 생명 주기
            
- 전통방식
    - html 태그로 시작해서 html 태그로 끝나는 완전한  HTML을 서버로부터 전송받아 웹페이지 전체를 처음부터 다시 렌더링하는 방식으로 동작
    - 화면이 전환되면 서버로부터 새로운 HTML을 전송받아 웹페이지 전체를 처음부터 다시 렌더링
- 장점 (전통방식과 비교)
    - 변경할 부분을 갱신하는데 필요한 데이터만 서버로부터 전송받기 때문에 불필요한 데이터 통신이 발생하지 않음
    - 변경할 필요가 없는 부분은 다시 렌더링 하지 않기 때문에 화면이 순간적으로 깜빡이는 현상이 없음
    - 클라이언트와 서버와의 통신이 비동기 방식으로 동작하기 때문에 서버에게 요청을 보낸 이후 블로킹이 발생하지 않음
    - 스크립트나 스타일 시트는 한 번만 요청하면 되므로 서버에 대한 연결을 줄여줌
    - 상태를 페이지에서 관리 할 수 있음
        - 메인 컨테이너 페이지가 다시 로드되지 않기 때문에 JavaScript의 변수와 DOM의 상태가 유지
    - SPA의 대부분의 장점과 같음
- 단점
    - 동적 웹 페이지는 북마크하기 어려움
    - 브라우저에서 JavaScript가 비활성화된 경우 작동하지 않음
    - 일부 웹 크롤러는 JavaScript를 실행하지 않으며 JavaScript에 의해 로드된 콘텐츠를 볼 수 없음
    - SPA의 대부분의 단점과 같음

## 18. **JSONP가 어떻게 동작하는지(그리고 Ajax와 어떻게 다른지)를 설명하세요**

- 동일참조원칙(Same-origin policy, SOP)
    - 웹페이지가 전달된 서버와 동일한 도메인의 서버로부터 전달된 데이터는 문제없이 처리할 수 있음
    - 보안상의 이유로 다른 도메인(http와 https, 포트가 다르면 다른 도메인으로 간주한다)으로의 요청(크로스 도메인 요청)은 제한
- SOP 우회방법 3가지
    - **웹서버의 프록시 파일**
        - 프록시(Proxy) : 서버에 원격 서버로부터 데이터를 수집하는 별도의 기능을 추가
    - JSONP(JSON with Padding)
        - script 태그의 원본 주소에 대한 제약은 존재하지 않기 때문에 이것을 이용하여 다른 도메인의 서버에서 데이터를 수집하는 방법
        - 자신의 서버에 함수를 정의하고 다른 도메인의 서버에 얻고자 하는 데이터를 인수로 하는 함수 호출문을 로드하는 것
            
            ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/995fa3b4-18fa-4149-89e4-ec5f8ae984e1/Untitled.png)
            
        - 보안 문제로 인해 JSONP는 [CORS](https://ko.wikipedia.org/w/index.php?title=%ED%81%AC%EB%A1%9C%EC%8A%A4_%EC%98%A4%EB%A6%AC%EC%A7%84_%EB%A6%AC%EC%86%8C%EC%8A%A4_%EC%85%B0%EC%96%B4%EB%A7%81&action=edit&redlink=1)로 대체
        - 예시
            - 외부 서비스 `http://server.example.com/Users/1234`에서 사람 Foo의 기록을 JSON 포맷으로 반환한다 하자. 다음과 같은 JSON 포맷을 볼 수 있을 것이다.
            
            ```jsx
            {
                **"Name"**: "Foo",
                **"Id"**: 1234,
                **"Rank"**: 7
            }
            ```
            
            - 이 데이터를 불러오기 위해 다음과 같이 JavaScript의 직접적인 HTTP 통신을 하면 오류가 발생한다.
            
            ```jsx
            **var** xmlhttp = **new** XMLHttpRequest();
            xmlhttp.open('GET', 'http://server.example.com/Users/1234', **true**);
            xmlhttp.onload = **function** () {
              console.log('Retrieved Data: ' + xmlhttp.responseText);
            };
            xmlhttp.send(); *// -> 교차 참조 요청 차단*
            ```
            
            - 반면 다음과 같이 script 태그에 JSON 데이터를 직접적으로 삽입하면 JSON 데이터를 교차 참조 정책에 관계 없이 불러올 수 있지만 JavaScript 문법 오류가 발생한다.
            
            ```jsx
            <**script** type="application/javascript"
                    src="http://server.example.com/Users/1234">
            </**script**>
            ```
            
            - 이는 웹 브라우저의 JavaScript 엔진이 변수, 상수 정의 등의 특정한 상황 없이 나오는 중괄호 문법을 block으로 해석하기 때문이다.
            - JSONP는 이러한 웹 브라우저의 특성을 이용해, JSON 데이터를 클라이언트가 지정한 콜백 함수를 호출하는 유효한 JavaScript 문법으로 감싸 클라이언트에 전송한다.
            - 클라이언트가 'parseResponse'라는 함수를 JSONP 요청의 콜백 함수로 지정하였다고 하면, 다음과 같은 HTML 태그가 문서에 삽입된다.
            
            ```jsx
            <**script** type="application/javascript"
                    src="http://server.example.com/Users/1234?callback=parseResponse">
            </**script**>
            ```
            
            - 외부 서비스 server.example.com은 다음과 같이 JSON 데이터를 패딩하여 클라이언트에 보낸다.
            
            ```jsx
            parseRespo**nse**({**"Name"**: "Foo", **"Id"**: 1234, **"Rank"**: 7});
            ```
            
            - 웹 브라우저는 이 데이터를 유효한 JavaScript 프로그램으로 받아들여 실행하고, 콜백 함수인 parseResponse가 실행되며 받아온 데이터를 처리할 수 있게 된다.
    - **Cross-Origin Resource Sharing(**CORS)
        - HTTP 헤더에 추가적으로 정보를 추가하여 브라우저와 서버가 서로 통신해야 한다는 사실을 알게하는 방법
        - 최신 브라우저에서만 동작하며 서버에 HTTP 헤더를 설정해 주어야 함

## 19. **JavaScript 템플릿을 사용한 적이 있나요? 사용해봤다면, 어떤 라이브러리를 사용했나요?**

- JSX
    - React에서 사용
        - 자바스크립트 확장문법
        - XML과 비슷
        - 작성된 코드는 브라우저에서 실행되기 전에 코드가 번들링되는 과정에서 바벨을 사용하여 일반 자바스크립트 형태의 코드로 변환
        - HTML 태그 뿐 아니라 컴포넌트도 작성가능
        - 예
        
        ```jsx
        // JSX
        
        class Hello extends React.Component {
          render() {
            return <div>Hello {this.props.toWhat}</div>;
          }
        }
        
        // JSX 안쓸때
        
        class Hello extends React.Component {
          render() {
            return React.createElement('div', null, `Hello ${this.props.toWhat}`);
          }
        }
        ```
        
- 템플릿 리터럴(Template Literal)
    - 라이브러리에 의존하지 않고 템플릿을 만드는 방법
    - ES6 도입
    - Multi-line 문자열, 표현식 삽입, tagged template 등 다양한 문자열 처리 가능
    - 백틱 ` 문자 사용
    - 활용
        - 멀티라인 문자열
            - 일반 문자열 내에서는 줄바꿈(개행) 허용되지 않음
            - 이스케이프 문자 \n
        - 표현식 삽입
            - `${ }` 표현식을 감싸서 사용

## 20. 호이스팅

- 결론
    - 함수안에 있는 선언들을 모두 끌어올려서 해당 함수 유효 범위의 최상단에 선언하는 것
- 설명
    - 자바스크립트 함수는 실행되기 전에 함수 안에 필요한 변수값들을 모아서 유효범위 최상단에 선언함
        - 자바스크립트 Parser가 함수 실행 전 해당 함수를 한 번 훑음
        - 함수 안에 존재하는 변수/함수선언에 대한 정보를 기억하고 있다가 실행시킴
        - 유효범위 : 함수 블록 안에서 유효
        - 실제로 코드가 끌어올리지는 것은 아님
    - var, let, const 변수/함수 선언과 함수 선언문에서 호이스팅이 일어난다
        - var, let, const 변수/함수의 선언만 위로 끌어 올려지며 할당은 끌어올려지지 않음
        - let 선언과 동시에 TDZ에 들어가서 초기화가 필요한 별도의 상태로 관리
        - const는 선언과 동시에 초기화, 할당까지 이뤄져야함
        - let, const, 함수표현문은 호이스팅이 일어나지 않는 것처럼 동작
    - 우선순위
        - 변수선언이 함수선언보다 더 위로 끌어올려짐
        - 값이 할당되어 있지 않은 변수의 경우, 함수선언문이 변수를 덮어씀
        - 값이 할당되어 있는 변수의 경우, 변수가 함수선언문을 덮어씀
    - 주의사항
        - 코드의 가독성과 유지보수를 위해 호이스팅이 일어나지 않도록 함
    - 확장개념
        - 변수생성단계
            - 선언 : 스코프와 변수 객체가 생성되고, 스코프가 변수 객체를 참조
            - 초기화 : 변수 객체 값을 위한 공간을 메모리에 할당하며 할당되는 값은 undefined임
            - 할당 : undefined로 초기화된 변수 객체에 값을 할당
        - TDZ(Temporal Dead Zone)
            - 선언은 되어있지만 초기화가 되지 않아 이를 위한 자리가 메모리에 준비되어 있지 않은 상태
            - var : 선언과 동시에 초기화, 즉 선언과 동시에 undefined 할당
            - let, const는 선언만 될 뿐 초기화는 변수 선언문에 도달했을 때 이루어지므로 초기화 이전에 변수에 접근하면 참조에러(Reference Error) 발생
- 요약
    - 함수안에 있는 var 선언과 함수선언문을 함수 유효범위의 최상단으로 끌어올리는 것
- 참조
    - [https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html](https://gmlwjd9405.github.io/2019/04/22/javascript-hoisting.html)
    - [https://yceffort.kr/2020/05/var-let-const-hoisting](https://yceffort.kr/2020/05/var-let-const-hoisting)
    - [https://velog.io/@holim0/Front-End-면접-질문-대비-Part1-hoisting-closure-this](https://velog.io/@holim0/Front-End-%EB%A9%B4%EC%A0%91-%EC%A7%88%EB%AC%B8-%EB%8C%80%EB%B9%84-Part1-hoisting-closure-this)
    
    기초부터 완성까지 프론트엔드

## 21. event bubbling에 대해 설명하세요.

- 이벤트 전파
    - DOM 트리 상에 존재하는 DOM 요소 노드에서 발생한 이벤트는 DOM 트리를 통해 전파
    - 생성된 이벤트 객체는 이벤트를 발생시킨 DOM 요소인 이벤트 타겟을 중심으로 DOM 트리를 통해 전파
        
        ![https://poiemaweb.com/img/eventflow.svg](https://poiemaweb.com/img/eventflow.svg)
        
    - 3단계
        - 캡쳐링 단계 : 이벤트가 상위 요소에서 하위 요소 방향으로 전파
        - 타겟 단계 : 이벤트가 이벤트 타겟에 도달
        - 버블링 단계 : 이벤트가 하위 요소에서 상위 요소 방향으로 전파
            - 이벤트가 제일 깊은 곳에 있는 요소에서 시작해 부모 요소를 거슬러 올라가며 발생하는 모양이 마치 물속 거품(bubble)과 닮았기 때문
        - capture 옵션
            - 
            - `false`이면(default 값) 핸들러는 버블링 단계에서 동작
            - `true`이면 핸들러는 캡처링 단계에서 동작
        
        ```jsx
        elem.addEventListener(..., {capture: true})
        // 아니면, 아래 같이 {capture: true} 대신, true를 써줘도 됩니다.
        elem.addEventListener(..., true)
        ```
        
    - 주의
        - 버블링으로 전파되지 않는 이벤트
            - 포커스 : focus/blur
            - 리소스 : load/unload/abort/error
            - 마우스 : mouseenter/mouseleave
    - 작동 방식
        - 같은 요소와 같은 단계에 설정한 리스너는 설정한 순서대로 동작
    - 캡처링 단계는 거의 쓰이지 않고, 주로 버블링 단계의 이벤트만 다뤄지는 이유
        - 현실에서 사고가 발생하면 지역 경찰이 먼저 사고를 조사합니다. 그 지역에 대해 가장 잘 아는 기관은 지역 경찰이기 때문입니다. 추가 조사가 필요하다면 그 이후에 상위 기관이 사건을 넘겨받습니다.
        - 이벤트 핸들러도 이와 같은 논리로 만들어졌습니다. 특정 요소에 할당된 핸들러는 그 요소에 대한 자세한 사항과 무슨 일을 해야 할지 가장 잘 알고 있습니다. `<td>`에 할당된 핸들러는 `<td>`에 대한 모든 것을 알고 있기 때문에 `<td>`를 다루는데 가장 적합합니다. 따라서 `<td>`를 다룰 기회를 이 요소에 할당된 핸들러에게 가장 먼저 주는 것입니다.
- 참조
    - [https://ko.javascript.info/bubbling-and-capturing](https://ko.javascript.info/bubbling-and-capturing)
    - 모던 자바스크립트 Deep Dive

## 22. "attribute"와 "property"의 차이점은 무엇인가요?

- 브라우저
    - 브라우저는 웹페이지를 만나면 HTML을 읽어(파싱(parsing)) DOM 객체를 생성
    - DOM 객체를 만들 때 HTML *표준* 속성(id 등)을 인식하고, 이 표준 속성을 사용해 DOM 프로퍼티를 만듬
- HTML attribute(속성) vs DOM property(프로퍼티)
    1. element node object에는 HTML attribute에 대응하는 DOM property가 존재
        - 주의 : 속성-프로퍼티가 항상 일대일로 매핑되지는 않음
    2. HTML attribute
        1. 역할 : HTML 요소의 초기 상태를 지정하는 것
        2. 표준 속성이 아닌 경우 아래의 메서드를 사용해 접근할 수 있음
            1. 메소드
                - `elem.hasAttribute(name)` – 속성 존재 여부 확인
                - `elem.getAttribute(name)` – 속성값을 가져옴
                - `elem.setAttribute(name, value)` – 속성값을 변경함
                - `elem.removeAttribute(name)` – 속성값을 지움
            2. 예
                1.  `getAttribute('About')` – 첫 번째 글자가 대문자 A이지만, HTML 안에서는 모두 소문자가 되어 속성은 대·소문자를 구분하지 않음
                2. 어떤 값이든 속성에 대입할 수 있지만, 최종적으론 문자열로 바뀜
    3. DOM property
        1. 사용자가 입력한 최신 상태는 HTML attribute에 대응하는 element node의 DOM property가 관리
        2. 사용자의 입력에 의한 상태 변화에 반응하여 최신상태 유지
        3. DOM 프로퍼티와 메서드는 일반 자바스크립트 객체처럼 행동
    4. 비교표
    
    |  | 속성 | 프로퍼티 |
    | --- | --- | --- |
    | 타입 | 문자열 | 모든 타입 가능 |
    | 이름 | 대·소문자 구분하지 않음 | 대·소문자 구분 |
    1. 주의
        1. 비표준 속성을 사용해 코드를 작성했는데 나중에 그 속성이 표준으로 등록되게 되면 문제가 발생
        2. 충돌 상황을 방지하기 위한 속성인 [data-*](https://html.spec.whatwg.org/#embedding-custom-non-visible-data-with-the-data-*-attributes)
        3. **’data-'로 시작하는 속성 전체는 개발자가 용도에 맞게 사용하도록 별도로 예약됩니다. `dataset` 프로퍼티를 사용하면 이 속성에 접근할 수 있음**
        4. `elem`에 이름이 `"data-about"`인 속성이 있다 `elem.dataset.about`을 사용해 그 값을 얻을 수 있음
1. 참조
    1. [https://ko.javascript.info/dom-attributes-and-properties](https://ko.javascript.info/dom-attributes-and-properties)
    2. 모던 자바스크립트 Deep Dive

## 23. 내장 JavaScript 객체를 확장하는 것이 좋은 생각이 아닌 이유는 무엇인가요?

- 네이티브 프로토타입은 수정할 수 있음
    - 예시
    
    ```jsx
    String.prototype.show = function() {
      alert(this);
    };
    
    "BOOM!".show(); // BOOM!
    ```
    
    - 네이티브 프로토타입을 수정하는 것은 추천하지 않음
        - 프로토타입은 전역으로 영향을 미치기 때문에 프로토타입을 조작하면 기존 코드와 충돌이 날 가능성이 큼
        - 두 라이브러리에서 동시에 `String.prototype.show` 메서드를 추가하면 한 라이브러리의 메서드가 다른 라이브러리의 메서드를 덮어씀
        - 예외
            - 모던 프로그래밍에서 네이티브 프로토타입 변경을 허용하는 경우 : 폴리필을 만들 때
                - 폴리필은 자바스크립트 명세서에 있는 메서드와 동일한 기능을 하는 메서드 구현체를 의미
                - 명세서에는 정의되어 있으나 특정 자바스크립트 엔진에서는 해당 기능이 구현되어있지 않을 때 폴리필을 사용
                - 폴리필을 직접 구현하고 난 후, 폴리필을 내장 프로토타입에 추가할 때만 네이티브 프로토타입을 변경
- 참조
    
    [https://ko.javascript.info/native-prototypes](https://ko.javascript.info/native-prototypes)

## 24. document load 이벤트와 document DOMContentLoaded 이벤트의 차이점은 무엇인가요?

- HTML 문서의 생명주기의 3가지 주요 이벤트
    - DOMContentLoaded
        - 브라우저가 HTML을 전부 읽고 DOM 트리를 완성하는 즉시 발생
        - 이미지 파일(`<img>`)이나 스타일시트 등의 기타 자원은 기다리지 않음
        - 활용
            - DOM이 준비된 것을 확인한 후 원하는 DOM 노드를 찾아 핸들러를 등록해 인터페이스를 초기화할 때
        - 특징
            - `<script>...</script>`나 `<script src="..."></script>`를 사용해 삽입한 스크립트는 DOMContentLoaded가 실행되는 것을 막으므로 브라우저는 이 스크립트가 실행되길 기다림
                - 이유
                    - `<script>`에 있는 스크립트가 DOM 조작 관련 로직을 담고 있을 수 있기 때문에 이런 방지책이 만들어 졌음
            - `DOMContentLoaded`는 실행되어도 이미지를 비롯한 기타 리소스들은 여전히 로드 중일 수 있음
        - 주의
            - **DOMContentLoaded를 막지 않는 스크립트**
                - 위와 같은 규칙엔 두 가지 예외사항이 있음
                - `async` 속성이 있는 스크립트는 `DOMContentLoaded`를 막지 않음
                    - 페이지 구성이 끝난 후에 async 스크립트 다운로딩이 끝난 경우, `DOMContentLoaded`는 async 스크립트 실행 전에 발생할 수 있음
                    - async 스크립트가 짧아서 페이지 구성이 끝나기 전에 다운로드 되거나 스크립트가 캐싱처리 된 경우, `DOMContentLoaded`는 `async` 스크립트 실행 후에 발생할 수도 있음
                    - async, defer
                    
                    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a2025b7d-5528-4819-b159-b2efaee18934/Untitled.png)
                    
                    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/62af946d-de1d-4003-9fbb-fda78c235280/Untitled.png)
                    
                - `document.createElement('script')`로 동적으로 생성되고 웹페이지에 추가된 스크립트는 `DOMContentLoaded`를 막지 않음
    - load
        - HTML로 DOM 트리를 만드는 게 완성되었을 뿐만 아니라 이미지, 스타일시트 같은 외부 자원도 모두 불러오는 것이 끝났을 때 발생
        - 활용
            - 이미지 사이즈를 확인할 때 등. 외부 자원이 로드된 후이기 때문에 스타일이 적용된 상태이므로 화면에 뿌려지는 요소의 실제 크기를 확인할 수 있음
        - 특징
            - 페이지를 비롯한 이미지 등의 자원 전부가 모두 불러와졌을 때 `window` 객체에서 실행됨
            - 모든 자원이 로드되는 걸 기다리기에는 시간이 오래 걸릴 수 있으므로 이 이벤트는 잘 사용되지 않음
    - beforeunload/unload
        - 사용자가 페이지를 떠날 때 발생
        - 활용
            - `beforeunload` – 사용자가 사이트를 떠나려 할 때, 변경되지 않은 사항들을 저장했는지 확인시켜줄 때
            - `unload` – 사용자가 진짜 떠나기 전에 사용자 분석 정보를 담은 통계자료를 전송하고자 할 때
        - 특징
            - 사용자가 최종적으로 사이트를 떠날 때 `window` 객체에서 발생
            - `unload` 이벤트 핸들러에선 지연을 유발하는 복잡한 작업이나 사용자와의 상호작용은 할 수 없기때문에 `unload` 이벤트는 아주 드물게 사용됨
- 참조
    - [https://ko.javascript.info/script-async-defer](https://ko.javascript.info/script-async-defer)
    - [https://ko.javascript.info/onload-ondomcontentloaded](https://ko.javascript.info/onload-ondomcontentloaded)

## 25. ==와 ===의 차이점은 무엇인가요?

- 비교연산자
    - == : 동등 비교
        - 좌항과 우항의 피연산자를 비교할 때 먼저 암묵적 타입 변환을 통해 타입을 일치시킨 후 비교
    - === : 일치 비교
        - 좌항과 우항의 피연산자가 타입과 값이 같을 때 true를 반환
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e7618cbf-77db-47a7-a3ce-4b6d12f440af/Untitled.png)
        
    - 개발자의 의도와는 상관없이 자바스크립트 엔진에 의해 암묵적으로 타입 자동 변환되기도함
        - 타입스크립트 도입 필요
- 참조
    
    모던 자바스크립트 Deep Dive

## 26. JavaScript와 관련하여 same-origin 정책을 설명하세요

- SOP(Same Origin Policy) : 동일 출처 정책
    - 브라우저 내 탭과 창은 대개 서로의 정보를 알 수 없음
    - 그런데 자바스크립트를 사용해 한 창에서 다른 창을 열 때는 예외가 적용
    - 이 경우에도 도메인이나 프로토콜, 포트가 다르다면 페이지에 접근할 수 없음
    - 자바스크립트는 스크립트를 포함하고 있는 문서와 같은 출처의 문서에 있는 window와 Document 객체의 속성만을 사용할 수 있음
    - 한 웹사이트내에서만 자원을 접근할 수 있기 때문에 다른 웹사이트의 이미지나 글을 가져올 수 없음
    - **예외적인 경우**를 두었고 그 중 하나가 바로 **CORS 조항을 지킨 자원**
- Origin
    - 출처 : PROTOCOL + HOST + PORT
        - 세가지 요소들이 전부 같다 = 같은 출처 (Same Origin)
        - 세가지 중 하나라도 틀리다 = 다른 출처 (Cross Origin)
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/da16dc49-0409-48d5-b668-86d5c5aeddd5/Untitled.png)
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/549ecbc8-8949-4e1d-b754-dc21480ef1d7/Untitled.png)
    
- 출처
    - [https://velog.io/@sj950902/CORS와-SOP에-대해-알아보자-1탄](https://velog.io/@sj950902/CORS%EC%99%80-SOP%EC%97%90-%EB%8C%80%ED%95%B4-%EC%95%8C%EC%95%84%EB%B3%B4%EC%9E%90-1%ED%83%84)

## 27. 다음이 작동하게 만들어보세요.

```js
duplicate([1, 2, 3, 4, 5]); // [1,2,3,4,5,1,2,3,4,5]
```

```js
duplicate([1, 2, 3, 4, 5]); // [1,2,3,4,5,1,2,3,4,5]
```

## 28. 왜 Ternary expression이라고 부르고, "Ternary"라는 단어는 무엇을 나타내나요?

- Ternary Operator 삼항 조건 연산자
    - 자바스크립트의 유일한 삼항 연산자
    - 형식
        - 조건식 ? 조건식이 true일 때 반환할 값 : 조건식이 false일 때 반환할 값
    - if else문과 차이
        - 삼항 조건 연산자 표현식은 값처럼 사용할 수 있지만 if else 문은 값처럼 사용 불가
- 삼항 조건 연산자 표현식은 값으로 평가할 수 있는 표현식인 문
    
    
- 표현식 expression
    
    값으로 평가될 수 있는 문
    
    표현식이 평가되면 새로운 값을 생성하거나 기존값을 참조
    
- 문 statement
    - 프로그램을 구성하는 기본 단위이자 최소 실행 단위
    - 여러개의 토큰으로 구성
- 토큰
    - 문법적으로 더이상 나눌 수 없는 코드의 기본 요소
    - 예) 식별자, 연산자 등
- 출처
    
    모던 자바스크립트 Deep Dive

## 29. "use strict"; 이 무엇인가요? 사용시 장단점이 무엇인가요?

- strict mode
    - ES5부터 추가됨
    - 자바스크립트 언어의 문법을 좀 더 엄격히 적용하여 오류를 발생시킬 가능성이 높거나 자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 명시적인 에러를 발생
    - ESLint를 사용하여 유사한 효과 얻을 수 있음
    - 적용방법
        - 전역의 선두 또는 함수 몸체의 선두에 `‘use strict’;` 를 추가
        - 전역과 함수단위로 적용하는 것은 비추
        - 즉시 실행함수로 감싼 스크립트 단위로 적용하는 것이 바람직
    - strict mode가 발생시키는 에러
        - 암묵적 전역
            - 선언하지 않은 변수를 참조하면 ReferenceError 발생
        - 변수, 함수, 매개변수의 삭제
            - delete 연산자로 삭제하면 SyntaxError 발생
        - 매개변수 이름의 중복
            - SyntaxError 발생
        - with 문의 사용
            - SyntaxError 발생
            - with 문은 전달된 객체를 스코프 체인에 추가
            - 객체이름을 생략할 수 있어서 간단하지만 성능과 가독성이 나쁨
    - strict mode 적용에 의한 변화
        - 일반함수의 this
            - 함수를 일반 함수로서 호출하면 this에 undefined가 바인딩됨
            - 생성자 함수가 아닌 일반함수 내부에서는 this를 사용할 필요가 없기 때문
            - 에러는 발생하지 않음
        - arguments 객체
            - 매개변수에 전달된 인수를 재할당해 변경해도 arguments 객체에 미반영됨
- 출처
    - 모던 자바스크립트 Deep Dive

## 30. 100까지 증가하면서 3의 배수에는 fizz를 출력하고, 5의 배수에는 buzz를 출력하고, 3과 5의 배수에는 fizzbuzz를 출력하는 for loop를 만드세요.

```jsx
function solution(num) {
  for (let i = 1; i <= num; i++){
    let answer = '';
    if (i % 3 === 0) {
      answer += 'fizz';
    }
    if (i % 5 === 0) {
      answer += 'buzz';
    }
    console.log(i, answer);
  }
}
console.log(solution(100));
```

## 31. Single page app이 무엇인지 설명하고 SEO-friendly하게 만드는 방법을 설명하세요

- SPA****(Single Page Application)****
    - 서버로부터 새로운 페이지를 불러오지 않고 현재의 페이지를 동적으로 다시 작성함으로써 사용자와 소통하는 웹 애플리케이션이나 웹사이트
    - 현재의 HTML을 고정하고 변경되는 부분에 대해서만 서버에서 불러와 클라이언트 사이드에서 렌더링하는 방식
    - 장점
        - **페이지 로딩속도가 빠름**
    - 단점
        - **최초 페이지 로딩속도가 느림**
            - 클라이언트가 최초로 서버에 요청할 때 모든 데이터를 가져오기 때문
        - **SEO에 적합하지 않을 수 있음**
- SEO(Search Engine Optimization)
    - 웹사이트 속도가 빨라 사용자 경험 측면에서 우수한 SPA는 사실 SEO친화적이지 않음
    - SPA는 하나의 페이지에 여러 페이지를 클라이언트 사이드에서 자바스크립트로 구현하는 방식이기 때문에 자바스크립트를 읽지 못하는 검색엔진에 대해서는 크롤링이 안되어 색인이 되지 않는 문제가 발생할 수 있음
- SEO 해결방법
    - SSR****(Server Side Rendering)****
        - SPA는 기본적으로 CSR (Client-Side Rendering) 방식으로 구현
        - SPA이지만 크롤링에 더 친화적인 SSR 방식(서버쪽에서 렌더링 준비를 끝마친 상태로 클라이언트에 전달하는 방식)으로 사이트를 구축하는 것이 SEO의 관점에서 적합
        - 대표적인 SSR 프레임워크로는 React의 Next.js, Vue의 Nuxt
- 출처
    
    [https://www.ascentkorea.com/seo-for-spa/](https://www.ascentkorea.com/seo-for-spa/)

## 32. Promises와 그 Polyfill에 대한 당신의 경험은 어느 정도인가요?

- 프로미스의 생성
    - 프로미스는 Promise 생성자 함수를 통해 인스턴스화
    - Promise 생성자 함수는 비동기 작업을 수행할 콜백 함수를 인자로 전달받는데 이 콜백 함수는 resolve와 reject 함수를 인자로 전달
    
    ```jsx
    // Promise 객체의 생성
    const promise = new Promise((resolve, reject) => {
      // 비동기 작업을 수행한다.
    
      if (/* 비동기 작업 수행 성공 */) {
        resolve('result');
      }
      else { /* 비동기 작업 수행 실패 */
        reject('failure reason');
      }
    });
    ```
    
- 후속 처리 메소드
    - then
        - then 메소드는 두 개의 콜백 함수를 인자로 전달 받음
        - 첫 번째 콜백 함수는 성공(fulfilled, resolve 함수가 호출된 상태) 시 호출되고 두 번째 함수는 실패(rejected, reject 함수가 호출된 상태) 시 호출
        - **then 메소드는 Promise를 반환**
    - catch
        - 예외(비동기 처리에서 발생한 에러와 then 메소드에서 발생한 에러)가 발생하면 호출
        - catch 메소드는 Promise를 반환
    
- 폴리필
    - 바벨 사용
        - **Babel**은 **구 브라우저**에서도 최신자바스크립트 코드를 작동하도록 변환해주는 컴파일러(혹은 트랜스파일러)

## 33. Callback 대신에 Promise를 사용할 때의 장점과 단점은 무엇인가요?

- 장점
    - 콜백 사용시 콜백 헬로 인해 가독성 안좋음
        - 예
        
        ```jsx
        step1(function(value1) {
          step2(value1, function(value2) {
            step3(value2, function(value3) {
              step4(value3, function(value4) {
                step5(value4, function(value5) {
                    // value5를 사용하는 처리
                });
              });
            });
          });
        });
        ```
        
    - 비동기처리 중 발생한 에러의 처리가 가능
        - 예
    
    ```jsx
    try {
      setTimeout(() => { throw new Error('Error!'); }, 1000);
    } catch (e) {
      console.log('에러를 캐치하지 못한다..');
      console.log(e);
    }
    ```
    
    - 여러 개의 비동기 처리 쉽게 가능
        - Promise.all() : 병렬로 순서 보장
        
        ```jsx
        Promise.all([
          new Promise(resolve => setTimeout(() => resolve(1), 3000)), // 1
          new Promise(resolve => setTimeout(() => resolve(2), 2000)), // 2
          new Promise(resolve => setTimeout(() => resolve(3), 1000))  // 3
        ]).then(console.log) // [ 1, 2, 3 ]
          .catch(console.log);
        ```
        
        - Promise.race() : 병렬로 가장 먼저 처리된 프로미스가 resolve한 결과를 resolve
- 단점
    - 브라우저가 ES6(ES2015)를 지원하지 않으면 사용불가
- 참고
    
    [https://poiemaweb.com/es6-promise](https://poiemaweb.com/es6-promise)
    
    모던 자바스크립트 Deep Dive

## 34. JavaScript로 컴파일되는 언어로 JavaScript 코드를 작성하는 경우의 장단점은 무엇인가요?

- TypeScript
    - 특징
        - 타입스크립트는 마이크로소프트(MS)에서 개발
        - 자바스크립트의 상위 집합으로서 ECMA의 최신 표준을 충분히 지원
        - ES6의 새로운 기능들을 사용하기 위해 Babel과 같은 별도 트랜스파일러를 사용하지 않아도 됨
        - TS -> (컴파일(트랜스파일)) -> JS -> (실행)
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fcbd50f4-ba07-40e5-8e4a-7e43a48f2506/Untitled.png)
        
    - 자바스크립트와 비교
        - 타입스크립트는 정적 타입 언어이기 떄문에 컴파일 시간이 조금 걸리지만, 안정성이 보장
        - 자바스크립트는 동적 타입 언어이기 때문에 런타임 속도는 빠르지만 타입 안정성이 보장되지 않음
        
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ea807273-3d1a-47d0-907b-b14ec104c578/Untitled.png)
        
- CoffeeScript
- Dart
- 공통단점
    - 익숙하지 않은 개발자는 배워야함
    - 최신 자바스크립트에 비해 버전이 느릴 수 밖에 없음
    - 자료 풀이 작음
- 참조
    - [https://hnm1.tistory.com/entry/자바스크립트-언어-안에도-다른-언어가-있다-자바스크립트-파생언어-TypeScript-CoffeeScript-Dart](https://hnm1.tistory.com/entry/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%96%B8%EC%96%B4-%EC%95%88%EC%97%90%EB%8F%84-%EB%8B%A4%EB%A5%B8-%EC%96%B8%EC%96%B4%EA%B0%80-%EC%9E%88%EB%8B%A4-%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%ED%8C%8C%EC%83%9D%EC%96%B8%EC%96%B4-TypeScript-CoffeeScript-Dart)
    - https://medium.com/geekculture/typescript-vs-javascript-e5af7ab5a331
    - [https://choseongho93.tistory.com/319](https://choseongho93.tistory.com/319)

## 35. JavaScript 코드를 디버깅하기 위해 어떤 도구와 기술을 사용하나요?

- React and Redux
    - [React Devtools](https://github.com/facebook/react-devtools)
    - [Redux Devtools](https://github.com/gaearon/redux-devtools)
- JavaScript
    - [Chrome Devtools](https://hackernoon.com/twelve-fancy-chrome-devtools-tips-dc1e39d10d9d)
    - `debugger` statement
    - `console.log` debugging
- React Query

## 36. 오브젝트 속성이나 배열 항목을 반복할 때 사용하는 언어 구문은 무엇인가요?

- 배열
    - for ... of 문
        - 배열
            - 값 반환
    - Array.prototype.forEach
        - for문을 대체할 수 있는 고차 함수(함수를 인수로 전달받거나 함수를 반환하는 함수)
        - for문은 반복을 위한 변수를 선언해야하며, 조건식과 증감식으로 이루어져 있어서 함수형 프로그래밍과 맞지 않음
        - 내부에서 반복문을 통해 자신을 호출한 배열을 순회하면서 수행해야할 처리를 콜백 함수로 전달받아 반복 호출
    - Array.prototype.map
        - 자신을 호출한 배열의 모든 요소를 순회하면서 전달받은 콜백함수를 반복 호출하고, 콜백 함수의 반환값들로 구성된 새로운 배열을 반환
        - 원본 배열은 변경되지 않음
- 객체
    - Object.keys : 객체 자신의 열거가능한 프로퍼티 키를 배열로 반환
    - Object.values : 객체 자신의 열거가능한 프로퍼티 값을 배열로 반환
    - Object.entries : 객체 자신의 열거 가능한 프로퍼티 키와 값의 쌍의 배열을 배열에 담아 반환
- 공통
    - for ... in 문
        - 배열
            - index 반환
            - for ... in 문 비추
                - 일관된 순서로 요소를 방문하지 못할 수 있음
                - for, for.. of, forEach메서드 사용을 권장
        - 객체
            - 객체의 프로토타입 체인 상에 존재하는 모든 프로토타입의 프로토타입의 프로퍼티 중에서 프로퍼티 어트리뷰트의 값이 true인 프로퍼티를 순회하며 열거
            - 객체 프로퍼티를 열거할 때 순서를 보장하지 않으므로 주의
            - 하지만 대부분의 모던 브라우저는 순서를 보장하고 숫자(실제로는 문자열)인 프로퍼티 키에 대해서는 정렬
- 이터러블
    - iteration protocol
        - ES6에서 도입된 이터레이션 프로토콜은 iterable(순회 가능한) 데이터 컬렉션(자료구조)을 만들기 위해 ECMAScript 사양에 정의하여 미리 약속한 규칙
        - ES6에서는 순회 가능한 데이터 컬렉션을 이터레이션 프로토콜을 준수하는 이터러블로 통일하여 for..of문, 스프레드 문법, 배열 디스트럭처링 할당의 대상으로 사용할 수 있도록 일원화 함
    - iterable
        - 이터러블 프로토콜을 준수한 객체를 이터러블
        - Symbol.iterator를 프로퍼티 키로 사용한 메서드를 직접 구현하거나 프로토타입 체인을 통해 상속받은 객체
        - 배열은 Array.prototype의 Symbol.iterator 메서드를 상속받는 이터러블
            - Symbol.iterator 메서드를 직접 구현하지 않거나 상속받지 않은 일반 객체는 이터러블 프로토콜을 준수한 이터러블이 아님
            - 일반객체는 for... of 문으로 순회 불가하며, 스프레드 문법과 배열 디스트럭처링 할당의 대상으로 사용불가
        - 빌트인 이터러블
            - Array, String, Map, Set, TypedArray, arguments, DOM 컬렉션
    - 유사배열객체
        - 마치 배열처럼 인덱스로 프로퍼티 값에 접근할 수 있고, length 프로퍼티를 갖는 객체
        - 예
        
        ```jsx
        const arrayLike = {
        	0: 1,
        	1: 2,
        	length: 3
        }
        ```
        
    
    참고
    
    모던 자바스크립트 Deep Dive
    
    추가내용 
    
    - for가 가장 빠르지만 다른것 써도 상관없음
    - forEach : this 바인딩이 있음
    - 배열도 entries 가능
    - reflect라는 것이 있음
    
    ```jsx
    Reflect.has(obj, ‘name’)
    Reflect.get(obj, ‘name’)
    const obj = {};
    [obj.name](http://obj.name/)[10.name](http://10.name/)
    ```
    
    깨달음
    
    - 얕은 복사, 깊은 복사는 메소드 차이가 아니라 결과값으로 판단하는 것

## 37. mutable 객체와 immutable 객체 사이의 차이점을 설명하세요

- 자바스크립트의 7가지 데이터타입
    - 숫자, 문자열, boolean, null, undefined, Symbol, Object
    - 크게 2가지 타입으로 분류
        - 원시타입 primitive type
            - 변경 불가능한 값 immutable value
            - 원시값을 변수에 할당하면 변수에는 실제 값이 저장
            - 데이터 타입
                - 숫자, 문자열, boolean, null, undefined, Symbol
        - 객체타입 object/reference type
            - 변경 가능한 값 mutable value
            - 객체를 변수에 할당하면 변수에는 참조 값이 저장
            - 데이터 타입
                - 객체, 함수, 배열 등
- 원시 값을 갖는 변수의 값을 변경하려면 재할당 외에는 방법이 없음
- 객체는 변경 가능한 값
    - 객체를 할당한 변수는 재할당 없이 객체를 직접 변경 가능
    - 프로퍼티 추가, 갱신, 삭제 가능
    - 객체를 변경할 때마다 원시 값처럼 이전 값을 복사해서 새롭게 생성한다면 신뢰성 확보되지만 객체는 매우 클수도 있고, 복사해서 생성하는 비용이 많이 듬
    - 메모리의 효율적 소비가 어렵고 성능이 나빠짐
    - 객체 변경 방지 메소드
        - Object.freeze
            - 얕은 객체 동결
            - 중첩 객체까지 동결할 수는 없음
- 참고
    - 모던 자바스크립트 Deep Dive

## 38. 동기, 비동기 함수의 차이점을 설명하세요

- 비동기 함수
    - 현재 실행 중인 태스크가 종료되지 않은 상태라고 해도 다음 태스크를 곧바로 실행하는 방식
    - 타이머 함수, HTTP 요청, 이벤트 핸들러가 처리되는 방식
    - 실행 순서 보장하지 않음
        - 보완
            - 콜백, 프로미스, async await
        - 예
        - 
        
        ```jsx
        setTimeout(()=> console.log('1'),0)
        console.log('2')
        
        // 2
        // 1
        ```
        
- 동기 함수
    - 현재 실행 중인 태스크가 종료할 때까지 다음에 실행될 태스크가 대기하는 방식
    - 자바스크립트는 싱글 스레드 방식이므로 대기동안 블로킹(작업중단) 발생

## 39. 이벤트 루프란 무엇인가요? 콜 스택과 태스크 큐의 차이점은 무엇인가요?

- 자바스크립트는 싱글 스레드로 동작
    - 한번에 하나의 태스크만 처리
    - 브라우저는 많은 태스크가 동시에 처리되는 것처럼 보임
- 이벤트 루프
    - 자바스크립트의 동시성을 지원하는 것
    - 브라우저에 내장되어 있는 기능
    - 콜 스택에 현재 실행 중인 실행 컨텍스트가 있는지 태스크 큐에 대기중인 함수가 있는지 반복해서 확인
    - 콜 스택이 비어 있고, 태스크 큐에 대기 중인 함수가 있다면 이벤트 루프는 순차적으로 태스크 큐에 대기 중인 함수를 콜 스택으로 이동
        - 태스크 큐에 일시 보관된 함수들은 비동기 처리방식으로 동작
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/410b9169-4ee3-42e6-9553-44a062986bce/Untitled.png)
    
    - 콜스택
        - 함수를 호출하면 함수 실행 컨텍스트가 순차적으로 실행
        - 자바스크립트 엔진은 단 하나의 콜 스택을 사용하기 때문에 최상위 실행 컨텍스트가 종료되어 콜 스택에서 제거되지 전까지는 다른 어떤 태스크도 실행되지 않음
    - 태스크 큐
        - setTimeout 등과 같은 비동기 함수의 콜백함수 또는 이벤트 핸들러가 일시적으로 보관되는 영역
        - 마이크로 태스크 큐
            - 프로미스의 후속 처리 메서드의 콜백함수가 일시적으로 보관되는 영역(태스크 큐보다 우선)
- 출처
    
    [https://felixgerschau.com/javascript-event-loop-call-stack/](https://felixgerschau.com/javascript-event-loop-call-stack/)
    
    모던 자바스크립트 Deep Dive

## 40. function foo() {}와 var foo = function() {} 사이에서 foo 사용의 차이에 대해 설명하세요

- 함수 선언문과 함수 표현식 차이
    - 함수 선언문
        - 함수의 생성시점
            - 런타임 이전에 자바스크립트 엔진에 의해 먼저 실행
                - 런타임에 이미 함수 객체가 생성되어 있고 함수이름과 동일한 식별자에 할당까지 완료
                - 호이스팅
        - 함수 이름 생략 불가
        - 실행 후 완료값은 undefined
    - 함수 표현식
        - 함수의 생성시점
            - 변수에 할당되는 값이 함수 리터럴인 문이므로 할당문이 실행되는 시점 즉 런타임에 평가되므로 함수 표현식의 함수 리터럴도 할당문이 실행되는 시점에 평가되어 함수 객체가 됨
            - 함수 호이스팅이 아니라 변수 호이스팅이 됨
        - 실행 후 완료값은 생성된 함수 출력
- 참고
    - 모던 자바스크립트 Deep Dive
    

