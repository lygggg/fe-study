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

