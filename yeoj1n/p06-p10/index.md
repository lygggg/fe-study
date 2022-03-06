## 6. What's the difference between a variable that is: null, undefined or undeclared? How would you go about checking for any of these states?

null: 명시적으로 할당된 값
undefined: 할당되지 않은 값

```
// "use strict";
// function foo() {
//   x = 1; // ReferenceError
// }
// foo();
// console.log(x);

var foo;
console.log(foo); // undefined
console.log(foo === undefined); // true
console.log(typeof foo === "undefined"); // true
console.log(typeof null); // object

console.log(foo == null); // true
// null == undefined
console.log(foo === null); // false
```

## 7. What is a closure, and how/why would you use one?

클로저: 외부 함수가 반환된 후에도 외부 함수의 변수 범위 스코프에 접근할 수 있는 함수입니다.

```
function jane() {
  const name = 'jane';
  const mid = 'A';
  const final = 'B+';
return {
    midtermScore: () => mid,
    finaltermScore: () => final,
  }
}
jane().midtermScore(); // A
jane().finaltermScore(); // B+
```

## 8. Can you describe the main difference between a .forEach loop and a .map() loop and why you would pick one versus the other?

**forEach vs map**

공통점: 배열의 요소를 반복

차이점

forEach: 값을 반환하지 않는다.

단순 반복을 해야하는 경우 사용

map: 새로운 배열을 작성하여 반환한다.

```
const arr = [1,2,3];
const test = arr.forEach((item) => item + 1);

const arr2 = [1,2,3];
const test2 = arr.map((item) => item + 1);
```

## 9. What's a typical use case for anonymous functions?

익명함수: 즉시실행함수로 사용 -> 일부 코드를 캡슐화하기 때문에 선언된 변수가 전역 범위로 누출되지 않는다.

일회성 함수로 사용

다른 곳에서 사용할 필요없는 콜백함수로 사용.

## 10. How do you organize your code? (module pattern, classical inheritance?)

네임스페이스: 수많은 함수, 객체, 변수들로 이루어진 코드가 전역 유효범위를 어지럽히지 않고, 애플리케이션이나 라이브러리를 위한 하나의 전역 객체를 만들고 모든 기능을 이 객체에 추가하는 것을 말합니다.

ex) jQuery

```
var Module = function() {

  var privateKey = 0;
  function privateMethod() {
    return ++privateKey;
  }
  return {
    publicKey: privateKey,
    publicMethod: () => privateMethod();
  }
}

var obj1 = Module();
obj1.publicMethod();//1
obj1.publicMethod();//2

var obj2 = Module();
obj2.publicMethod();//1
obj2.publicMethod();//2
```

단점

- 전체적으로 코드량이 약간 더 많아지고 따라서 다운로드해야 하는 파일크기도 늘어난다.

- 전역 인스턴스가 단 하나뿐이기 때문에 코드의 어느 한 부분이 수정되어도 전역 인스턴스를 수정하게 된다.

즉, 나머지 기능들도 갱신된 상태를 물려받게 된다.

장점

- 점점 더 늘어만 가는 코드를 정리할때 널리 사용되며 자바스크립트 코딩패턴에서 널리 권장되는 방법이기도 하다.

Flux 아키텍처
