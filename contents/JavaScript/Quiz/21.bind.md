# Function.prototype.bind

이는 JS에서 특정 `this` 값과 선택적 초기 인자들을 가진 새로운 함수를 생성할 수 있게 해주는 메서드다.

## 주요 목적

1. this 값 바인딩으로 컨텍스트 보존

`bind`의 주요 목적은 함수의 `this`값을 특정 객체에 바인딩하는 것이다. <br />
`func.bind(thisArg)`를 호출하면, `func`와 동일한 본문을 가진다. <br />
하지만, `this`가 영구적으로 `thisArg`에 바인딩된 새 함수가 생성된다.

```javascript
const person = {
  name: "John",
  greet: function () {
    console.log(`Hello, ${this.name}!`);
  },
};

const greetFunction = person.greet;
// 이렇게 하면 this 컨텍스트가 손실됨
greetFunction(); // "Hello, undefined!"

const boundGreet = person.greet.bind(person);
// bind로 this를 person에 고정
boundGreet(); // "Hello, John!"
```

2. 인자의 부분 적용

`bind`는 새로운 함수에 대한 인자들을 미리 지정할 수 있게 해준다. <br />
`thisArg` 이후에 `bind`에 전달된 모든 인자들은 새로운 함수가 호출될 때, 인자 목록의 앞부분에 추가된다.

```javascript
function multiply(a, b) {
  return a * b;
}

// 첫 번째 인자를 2로 고정
const multiplyByTwo = multiply.bind(null, 2);
console.log(multiplyByTwo(4)); // 8
console.log(multiplyByTwo(5)); // 10
```

3. 메서드 차용

`bind`를 사용하면 한 객체의 메서드를 다른 객체에서 차용해 적용할 수 있다. <br />
이는 원래 그 객체와 함께 작동하도록 설계되지 않았더라도 가능하다.

`bind` 메서드는 특히 이벤트 핸들러, 콜백, 메서드 차용과 같이 함수가 특정 `this` 컨텍스트로 호출되어야 하는 시나리오에서 유용하다.

```javascript
const numbers = {
  array: [1, 2, 3],
  getNumbers() {
    return this.array;
  },
};

const data = {
  array: [4, 5, 6],
};

// numbers의 메서드를 data 객체에서 사용
const borrowedGetNumbers = numbers.getNumbers.bind(data);
console.log(borrowedGetNumbers()); // [4, 5, 6]
```

---

`Function.prototype.bind`는 특정 `this` 컨텍스트와 선택적으로 미리 설정된 인자를 가진 새 함수를 생성할 수 있게 해준다. <br />
`bind()`는 다른 함수에 전달하고자 하는 클래스의 메서드에서 `this` 값을 보존하는 데 가장 유용하다. <br />
`bind`는 화살표 함수를 사용하지 않고 정의된 레거시 React 클래스 컴포넌트 메서드에서 자주 사용됐었다.

```javascript
const john = {
  age: 42,
  getAge: function () {
    return this.age;
  },
};

console.log(john.getAge()); // 42

const unboundGetAge = john.getAge;
console.log(unboundGetAge()); // undefined

const boundGetAge = john.getAge.bind(john);
console.log(boundGetAge()); // 42

const mary = { age: 21 };
const boundGetAgeMary = john.getAge.bind(mary);
console.log(boundGetAgeMary()); // 21
```

위 예제에서 `getAge` 메서드가 호출 객체없이 호출될 때(`unboundGetAge` 처럼), `getAge()` 내부의 `this`가 전역 객체가 되어 값이 `undefined`가 된다. <br />
`boundGetAge`는 `this`가 `john`에 바인딩 되어 있어서 그에 해당한 `42`가 나온다.

## 콜백 사용

함수를 콜백으로 전달한다면, 함수 내부의 `this` 값은 실행 컨텍스트에 의해 결정되기에 예측할 수 없을 수 있다. <br />
`bind()`를 사용하면, 올바른 `this` 값이 유지되도록 보장할 수 있다.

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  },
};

const john = new Person('John Doe');

// Without bind(), `this` inside the callback will be the global object
setTimeout(john.greet, 1000); // Output: "Hello, my name is undefined"

// Using bind() to fix the `this` value
setTimeout(john.greet.bind(john), 2000); // Output: "Hello, my name is John Doe"
```

## 화살표 함수 사용

화살표 함수를 사용한다면, `bind` 대신에 클래스 메서드를 정의할 수도 있다. <br />
화살표 함수는 `this`값이 자신의 렉시컬 컨텍스트에 바인딩 된다.

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  greet = () => {
    console.log(`Hello, my name is ${this.name}`);
  };
}

const john = new Person("John Doe");
setTimeout(john.greet, 1000); // Output: "Hello, my name is John Doe"
```

## 함수의 부분 적용 (커링)

`bind`를 사용해 일부 인자가 미리 설정된 새로운 함수를 만들 수 있다. <br />
이를 부분 적용 또는 커링이라고 한다.

```javascript
function multiply(a, b) {
  return a * b;
}

// Using bind() to create a new function with some arguments pre-set
const multiplyBy5 = multiply.bind(null, 5);
console.log(multiplyBy5(3)); // Output: 15
```

## 메서드 차용

`bind`를 사용하면, 원래 그 객체와 함께 작동하도록 설계되지 않았더라도, 한 객체의 메서드를 다른 객체에 빌려 적용할 수 있다. <br />
이는 서로 다른 객체를 재사용하기 좋다.

```javascript
const person = {
  name: "John",
  greet: function () {
    console.log(`Hello, ${this.name}!`);
  },
};

const greetPerson = person.greet.bind({ name: "Alice" });
greetPerson(); // Output: Hello, Alice!
```
