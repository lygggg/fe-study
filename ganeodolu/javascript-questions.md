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

## 17. **JSONP가 어떻게 동작하는지(그리고 Ajax와 어떻게 다른지)를 설명하세요**

- 동일출처원칙(Same-origin policy, SOP)
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
            xmlhttp.send(); *// -> 교차 출처 요청 차단*
            ```
            
            - 반면 다음과 같이 script 태그에 JSON 데이터를 직접적으로 삽입하면 JSON 데이터를 교차 출처 정책에 관계 없이 불러올 수 있지만 JavaScript 문법 오류가 발생한다.
            
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

## 18. **JavaScript 템플릿을 사용한 적이 있나요? 사용해봤다면, 어떤 라이브러리를 사용했나요?**

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

## 19. 호이스팅

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
