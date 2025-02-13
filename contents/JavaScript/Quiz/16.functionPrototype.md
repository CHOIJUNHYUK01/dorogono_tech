# .call과 .apply 차이

### TL;DR

`.call`과 `.apply`는 둘 다 특정한 `this` 컨텍스트에서 실행하는 함수다. <br />
둘의 가장 큰 차이점은 매개변수를 받는 방식이다.

- call은 각 요소를 ,로 구분해서 받는다. <br />
- apply는 각 요소를 배열 형태로 받는다.

`add` 함수가 있다고 해보자. <br />
이 함수가 각각 `call`과 `apply`로 받는 방식이다.

```javascript
function add(a, b) {
  return a + b;
}

add.call(null, 1, 2); // 3
add.apply(null, [1, 2]); // 3
```

---

## Call vs. Apply

`.call`과 `.apply` 모두 함수를 호출하는데 사용된다. <br />
첫 번째 매개변수는 함수 내에서 `this` 값으로 사용된다. <br />
`.call`은 쉼표로 구분된 인수를, `.apply`는 배열로된 인수를 받는다.

ES6 문법에서는 스프레드 연산자를 사용해, 배열과 함께 `.call`을 사용할 수 있다.

```javascript
function add(a, b) {
  return a + b;
}

console.log(add.call(null, ...[1, 2])); // 3
```

## 컨텍스트 관리

```javascript
const person = {
  name: "John",
  greet() {
    console.log(`Hello, my name is ${this.name}`);
  },
};

const anotherPerson = { name: "Alice" };

person.greet.call(anotherPerson); // Hello, my name is Alice
person.greet.apply(anotherPerson); // Hello, my name is Alice
```

`anotherPerson`의 컨텍스트에서 실행을 한다.

## 함수 차용 (Function Borrowing)

`.call`과 `.apply`는 한 객체의 메서드를 빌려와서 다른 객체의 컨텍스트에서 사용할 수 있게 해준다. <br />
이는 함수를 인자(콜백)으로 전달할 때와 원래의 `this` 컨텍스트가 손실될 때 유용하다. <br />
`.call`과 `.apply`는 의도한 `this` 값으로 함수를 호출할 수 있게 해준다.

```javascript
function greet() {
  console.log(`Hello, my name is ${this.name}`);
}

const person1 = { name: "John" };
const person2 = { name: "Alice" };

greet.call(person1); // Hello, my name is John 출력
greet.call(person2); // Hello, my name is Alice 출력
```

## 객체의 메서드를 호출하는 대체 구문 (Alternative syntax)

`.apply`는 객체를 첫 번째 인자로 전달하고, 그 뒤에 일반적인 매개변수를 전달해 객체 메서드와 함께 사용될 수 있다.

```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

Array.prototype.apply(arr1, arr2); // arr1.push(4, 5, 6)와 동일
console.log(arr1); // [1, 2, 3, 4, 5, 6] 출력
```

1. 첫 번째 객체인 `arr1`이 `this` 값이 된다. <br />
2. `.apply`를 사용하기 때문에, `arr2`가 배열 형태의 인자로 사용되어, `arr1`에 `push()`가 호출된다. <br />
3. `Array.prototype.push.apply(arr1, arr2)`는 `arr1.push(...arr2)`와 동일하다. <br />
4. 명확하지 않을 수 있지만, `Array.prototype.push.apply(arr1, arr2)`는 `arr1`을 수정한다. <br />
5. 가능한 경우, 객체 지향적인 방식으로 메서드를 호출하는 것이 더 명확하다.

---

### .bind와의 차이점

`.call`과 `.apply`는 함수를 즉시 실행한다. <br />
단, `.bind`는 함수를 실행하지 않고, `this`가 바인딩된 새 함수를 반환한다. <br />
`.bind`는 `.call`과 같이 쉼표로 구분된 인자를 받는다.

`.bind`는 새로운 함수를 생성하기에, 추가 메모리를 사용한다. <br />
또한, 한 번만 바인딩 하면 되므로, 여러 번 재사용할 때 유용하다. <br />
`.call`과 `.apply`는 매번 `this`를 설정해야 한다.
