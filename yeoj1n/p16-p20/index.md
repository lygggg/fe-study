## 16. What's the difference between feature detection, feature inference, and using the UA string?

### Feature Detection

- 현재 브라우저에서 기능이 지원되는지 여부를 확인하기 위해 테스트를 실행하고, 조건부로 코드를 실행하여 지원/미지원을 감지하는 것
- 특징 감지를 사용하면 지원/미지원 브라우저 모두에게 기능을 제공할 수 있다.

```
if ('geolocation' in navigator) {
  // navigator.geolocation를 사용할 수 있습니다
} else {
  // 부족한 기능 핸들링
}
```

### Feature Inference

```
if (document.getElementsByTagName) {
  element = document.getElementById(id);
}
```

## 17. Explain Ajax in as much detail as possible.

### AJAX(AsynchronousJavaScriptAndXML)

**비동기적 자바스크립트 동작을 하는 기술을 통칭** => 자바스크립트를 사용하여 브라우저가 서버에게 비동기 방식으로 데이터를 요청하고, 서버가 응답한 데이터를 수신하여 웹페이지를 동적으로 갱신하는 프로그래밍 방식

Ajax가 나오기 전 웹페이지 렌더링 방식 -> HTML을 서버로 전달받아 웹페이지를 처음부터 다시 렌더링 하는 방식

### XMLHttpRequest

- XHR객체를 이용한 Ajax를 방식

```
  const responseReady = () => {
    try {
      if (httpRequest.readyState === XMLHttpRequest.DONE) {
        if (httpRequest.status === 200) {
			// 응답을 정상적으로 받음
          return httpRequest.responseText;
        } else {
          return Error('request에 문제가 있습니다.');
        }
      } else {
        return Error('request의 상태가 complete(4)가 아닙니다.');
      }
    }
    catch( e ) {
      return Error('Caught Exception: ' + e.description);
    }
  }

  httpRequest.open("GET", "/src/data.json");
  httpRequest.send();
})();

```

### fetch

대표적인 예시로 fetch API가 있다.
Promise와 함께 Ajax를 쉽게 사용하는 방식

```
fetch(resource, init)
    .then( callback )
    .catch( callback )
```

## 18. What are the advantages and disadvantages of using Ajax?

### 장점

- 변경할 부분을 갱신하는데 필요한 데이터만 전송받기 때문에 불필요한 데이터 통신이 발생하지 않는다.
- 변경할 필요가 없는 부분은 다시 렌더링하지 않아 화면이 깜박이는 현상이 발생하지 않는다.
- 서버에게 요청을 보낸 후 블로킹이 발생하지 않는다.

### 단점

- SPA의 단점
- Ajax는 클라이언트가 서버에 데이터를 요청하는 클라이언트 풀링 방식을 사용하므로, 서버 푸시 방식의 실시간 서비스는 만들 수 없습니다.
- Ajax로는 바이너리 데이터를 보내거나 받을 수 없습니다.
- Ajax 스크립트가 포함된 서버가 아닌 다른 서버로 Ajax 요청을 보낼 수는 없습니다.
- 클라이언트의 PC로 Ajax 요청을 보낼 수는 없습니다.

## 19. Explain how JSONP works (and how it's not really Ajax).

- CORS 해결하기 위한 방법이나 보안적 이슈가 있으니 사용하지말자

## 20. Have you ever used JavaScript templating? If so, what libraries have you used?

-

## 21. Explain "hoisting".

인터프리터가 변수와 함수의 메모리 공간을 선언 전에 미리 할당하는 것을 의미합니다

```
name = 'hello' // ReferenceError: Cannot access 'name' before initialization
let name = 'hi'
```

```
name = 'hello' // ReferenceError: Cannot access 'name' before initialization
var name = 'hi'
```
