## Explain event delegation

# 1주차

## 1. Explain event delegation

이벤트 위임이란 이벤트 리스너를 하위 요소에 추가하는 대신 상위 요소에 추가하는 기법이다.

동일한 이벤트를 여러 요소에 적용해야할 때, 상위 요소에 이벤트 핸들러를 하나만 할당하면 여러 요소를 한꺼번에 다룰 수 있다.

이벤트 버블링: 한 요소의 이벤트가 발생하면 이어서 부모의 이벤트 핸들러도 동작하는 현상

## 2. Explain how this works in JavaScript

this: 대부분은 함수를 호출한 방법에 의해 결정된다.

https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/this

## 3. Explain how prototypal inheritance works

기능 확장, 객체를 확장 시 사용할 수 있다.
부모에서 정의된 함수를 재정의없이 사용할 수 있다.

## 4. What do you think of AMD vs CommonJS?

### AMD(Asynchronous Module Definition)

- define 사용
- 클라이언트 사이드 개발에 더 적합하다. (비동기)

1. 동적 로딩
   페이지 렌더링을 방해하지 않으면서 필요한 파일만 로딩한다.
2. 의존성 관리
3. 모듈화
   스크립트 내부에서만 사용하는 변수, 함수를 전역공간에 두지 않고 return으로 외부에서 접근할 변수, 함수만 골라 노출시킨다.

RequireJS 예제

```
// 3. 모듈화
require(['js/util', 'js/Ajax','js/Event'], function (util, Ajax, Event) {

});
```

기본적으로 AMD는 순서를 보장하지 않으나 다음과 같은 방식으로 순서를 보장할 수는 있다.

```
// 동적로딩, 순서보장
    require(['js/first'], function (first) {
    require(['js/second'], function (second) {
        //
    });
```

### CommonJS

- module.exports 를 통해 모듈을 정의하고 require()함수를 통해 모듈을 호출한다.
- 노드에서 채택한 방식
- 서버사이드, 애플리케이션에서 개발의 용이를 위해 만들어졌다.

```
const $ = require('jquery');
const Z = require('zerocho');
module.exports = {
  a: $,
  b: Z,
};
```

### UMD(Universal Module Definition)

- CommonJS와 AMD를 통합하기 위한 패턴
  https://github.com/umdjs/umd/blob/master/templates/returnExports.js

### ES6방식

- import, export(default export, named export) 방식을 지원

## 5. Explain why the following doesn't work as an IIFE: function foo(){ }();. What needs to be changed to properly make it an IIFE?

(function foo(){}())
또는
(function foo(){})()

const foo = void (function bar(){
return 'foo'
}());
console.log(foo);//undefined
