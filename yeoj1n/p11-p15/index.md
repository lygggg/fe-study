## 11. What's the difference between host objects and native objects?

host objects: 호스트 환경에 정의된 객체
브라우저 환경: window, BOM(Browser Object Model), DOM(Document Object Model), XMLHttpRequest객체

native objects: ECMAScript ECMAScript 명세에 정의된 객체로 애플리케이션 전역의 공통 기능을 제공한다.
Object, Function,

## 12. Difference between: function Person(){}, var person = Person(), and var person = new Person()?

생성자

```
function Person(name) {
  this.name = name;
}

var person = new Person('John');
Object.create(Person.prototype);
```

https://ko.javascript.info/constructor-new#ref-1283

## 13. What's the difference between .call and .apply?

call과 apply는 함수를 호출하며, 첫번째 인자가 this가 된다.
그리고 두번째 인자부터 파라미터로 사용되며, call은 인수목록을 받고 apply는 인수 배열1개를 받는다.

```
const person = { name: 'Lee' };
const person2 = { name: 'Kim' };
const say = function(age) {
  console.log(`Hello, my name is ${this.name} and I'm ${age} years old.`)
}
say(20);
say.call(person, 20);
say.call(person2, 20);
say.apply(person, [20]);
say.apply(person2, [20]);
```

## 14. Explain Function.prototype.bind.

call과 apply와 달리 bind는 함수를 호출하지 않고 새로운 함수를 생성한다.
두번째 인자부터는 call, apply와 동일하게 파라미터로 사용된다.

```
const person = { name: 'Lee' };
function foo() {
  console.log(this.name);
}
let bar = foo.bind(person);
bar();
```

## 15. When would you use document.write()?

문서 전체의 내용을 지우고 문자열로 주어진 매개 변수 값으로 대체합니다
