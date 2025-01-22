# THIS

### TL;DR

`this`를 위한 쉬운 설명은 없다. <br />
자바스크립트 개념에서 가장 혼란스러운 것이다. <br />
다른 프로그래밍 언어와는 다르게 작동하기 때문이다. <br />
한 줄로 설명하자면, 이건 `함수가 실행되는 컨텍스트에 대한 동적 참조`라는 것이다.

`this`는 아래의 규칙을 따른다.

1. 함수를 호출할 때, `new` 키워드가 사용되면, 즉 함수가 생성자 함수로 사용된 경우, 함수 내부의 `this`는 새로 생성된 객체 인스턴스다. <br />
2. `this`가 클래스 생성자에서 사용되면, 생성자 내부의 `this`는 새로 생성된 객체 인스터스다. <br />
3. `apply()`, `call()`, `bind()`가 함수를 호출 및 생성할 때 사용되면, 함수 내부의 `this`는 인자로 전달된 객체다. <br />
4. 함수가 메서드로 호출(`obj.method()`) 된다면, `this`는 함수가 속성으로 있는 객체다. <br />
5. 함수가 자유 함수 호출로 실행되면, 즉 위의 조건들 없이 호출된 경우, 전역 객체가 된다. <br />
   브라우저에서 전역 객체는 `window` 객체다. <br />
   엄격모드에서는 `this`가 전역 객체 대신 `undefined`가 된다. <br />
6. 위의 규칙들 중 여러 개가 적용되는 경우, 더 높은 순위의 규칙이 이기고 `this` 값을 설정한다. <br />
7. 함수가 화살표 함수인 경우, 위의 모든 규칙을 무시하고 생성되는 시점의 주변 스코프에서 `this`값을 받는다.

---

## this 키워드

자바스크립트에서 `this`는 함수나 스크립트의 현재 실행 콘텍스트를 참조하는 키워드다. <br />
이건 자바스크립트의 기본적인 개념이며, `this`가 어떻게 작동하는지 이해하는 것은 견고하고 유지보수가 가능한 애플리케이션을 만드는 데 매우 중요하다.

### 전역 객체

글로벌 스코프에서 `this`는 전역 객체를 참조한다. <br />
`window` 객체는 브라우저나 Node.js 환경에서의 전역 객체다.

```javascript
console.log(this); // In a browser, this will log the window object (for non-strict mode).
```

### 일반 함수 호출

함수가 전역 컨텍스트에서 호출되거나 독립 실행 함수로 호출된다면, `this`는 전역 객체가 된다. <br />
엄격 모드에서는 `undefined`가 된다.

```javascript
function showThis() {
  console.log(this);
}

showThis(); // In non-strict mode: Window (global object). In strict mode: undefined.
```

### 메서드 호출

함수가 객체의 메서드로 호출될 때, `this`는 해당 메서드가 호출된 객체를 참조한다.

```javascript
const obj = {
  name: "John",
  showThis: function () {
    console.log(this);
  },
};

obj.showThis(); // { name: 'John', showThis: ƒ }
```

아래와 같이 하면 일반 함수 호출과 동일해지고, 메서드 호출이 아니다. <br />
`this`는 컨텍스트를 잃고 더 이상 `obj`를 가리키지 않는다.

```javascript
const obj = {
  name: "John",
  showThis: function () {
    console.log(this);
  },
};

const showThisStandalone = obj.showThis;
showThisStandalone(); // 비엄격 모드: Window (전역 객체), 엄격 모드: undefined
```

### 클래스 생성자와 메서드

클래스에서 `this`는 객체 메서드에서처럼 동작한다. <br />
클래스의 인스턴스를 참조한다.

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  showThis() {
    console.log(this);
  }
}

const person = new Person("John");
person.showThis(); // Person {name: 'John'}

const showThisStandalone = person.showThis;
showThisStandalone(); // `undefined` (클래스의 모든 부분이 엄격 모드이기 때문)
```

### this의 명시적 바인딩

`bind()`, `call()`, `apply()`를 사용해 함수의 `this`값을 명시적으로 설정할 수 있다.

```javascript
function showThis() {
  console.log(this);
}
const obj = { name: "John" };

showThis.call(obj); // { name: 'John' }
showThis.apply(obj); // { name: 'John' }

const boundFunc = showThis.bind(obj);
boundFunc(); // { name: 'John' }
```

### 화살표 함수

화살표 함수는 자신만의 `this` 컨텍스트를 갖지 않는다. <br />
대신 `this`는 렉시컬 스코프를 가지며, 이는 정의된 시점의 주변 스코프에서 상속받는다.

```javascript
const person = {
  name: "John",
  sayHello: () => {
    console.log(`Hello, my name is ${this.name}!`);
  },
};

person.sayHello(); // "Hello, my name is undefined!"
```

화살표 함수의 렉시컬 스코프 <br />
다음은 화살표 함수 내의 `this`는 자신을 감싸고 있는 컨텍스트의 `this`값을 가지므로, 어떻게 호출되는지에 따라 달라진다.

```javascript
const obj = {
  name: "John",
  showThis: function () {
    const arrowFunc = () => {
      console.log(this);
    };
    arrowFunc();
  },
};

obj.showThis(); // { name: 'John', showThis: ƒ }

const showThisStandalone = obj.showThis;
showThisStandalone(); // 비엄격 모드: Window (전역 객체), 엄격 모드: undefined
```

화살표 함수의 this 바인딩 제한 <br />
화살표 함수의 `this`값은 `bind()`, `apply()`, `call()` 메서드로 설정할 수 없고, 객체 메서드에서도 현재 객체를 가리키지 않는다.

```javascript
const obj = {
  name: "Alice",
  regularFunction: function () {
    console.log("Regular function:", this.name);
  },
  arrowFunction: () => {
    console.log("Arrow function:", this.name);
  },
};

const anotherObj = {
  name: "Bob",
};

// 일반 함수에서 call/apply/bind 사용
obj.regularFunction.call(anotherObj); // Regular function: Bob
obj.regularFunction.apply(anotherObj); // Regular function: Bob
const boundRegularFunction = obj.regularFunction.bind(anotherObj);
boundRegularFunction(); // Regular function: Bob

// 화살표 함수에서 call/apply/bind 사용 - this는 전역 스코프를 참조하며 수정할 수 없음
obj.arrowFunction.call(anotherObj); // Arrow function: undefined (엄격 모드에 따라 다름)
obj.arrowFunction.apply(anotherObj); // Arrow function: undefined (엄격 모드에 따라 다름)
const boundArrowFunction = obj.arrowFunction.bind(anotherObj);
boundArrowFunction(); // Arrow function: undefined (엄격 모드에 따라 다름)
```

### 이벤트 핸들러

DOM 이벤트 핸들러로 함수가 호출되면, `this`는 이벤트를 트리거한 요소를 참조한다.

```html
<!-- 버튼 요소가 로그에 출력됨 -->
<button id="my-button" onclick="console.log(this)">Click me</button>;
```

```javascript
document.getElementById("my-button").addEventListener("click", function () {
  console.log(this); // 버튼 요소가 로그에 출력됨
});
```

렉시컬 스코프를 사용한다. <br />
그래서 `call()`, `apply()`, `bind()`를 통해 `this` 컨텍스트를 정의하는 걸 방지한다. <br />
결과적으로 `addEventListener()`의 콜백 파라미터를 화살표 함수로 정의하면, 이벤트 핸들러에서 `this`가 제대로 바인딩되지 않는다.

```javascript
document.getElementById("my-button").addEventListener("click", () => {
  console.log(this); // Window / undefined (엄격 모드 여부에 따라 다름), 버튼 요소가 아님
});
```

### 정리

자바스크립트에서 `this`는 함수나 스크립트의 현재 실행 컨텍스트를 참조한다. <br />
사용되는 컨텍스트에 따라 그 값이 변한다. <br />
`this`가 어떻게 작동하는지 이해하는 것은 견고하고 유지보수 가능한 자바스크립트 코드를 작성하는 데 필수적이다.
