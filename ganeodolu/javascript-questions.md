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
