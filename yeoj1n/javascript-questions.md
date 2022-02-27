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

모듈 시스템을 구현하는 방법
CommonJS: 동기
AMD: 비동기

노션 링크

## 5. Explain why the following doesn't work as an IIFE: function foo(){ }();. What needs to be changed to properly make it an IIFE?

(function foo(){}())
또는
(function foo(){})()

const foo = void (function bar(){
return 'foo'
}());
console.log(foo);//undefined

## What's the difference between a variable that is: null, undefined or undeclared? How would you go about checking for any of these states?

## What is a closure, and how/why would you use one?

## Can you describe the main difference between a .forEach loop and a .map() loop and why you would pick one versus the other?

## What's a typical use case for anonymous functions?

## How do you organize your code? (module pattern, classical inheritance?)
