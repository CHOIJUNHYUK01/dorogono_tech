# Throttle

스로틀엔 두 가지 상태가 있다.

1. Idle <br />
   마지막 대기 시간 동안 스로틀된 함수가 호출되지 않은 상태다. <br />
   스로틀된 함수를 호출하면, 콜백 함수가 즉시 실행된다. <br />
   실행 후에는 `Active` 상태가 된다.

2. Active <br />
   마지막 대기 시간 내에 스로틀된 함수가 호출된 상태다. <br />
   대기 시간이 끝날 때까지 추가 호출은 콜백 함수를 실행하지 않는다.

구현에 필요한 요소가 있다. <br />

- 타이머: `setTimeout`을 사용한다. <br />
- 두 가지 상태만 있으므로, `boolean` 변수로 상태 관리가 가능하다.

---

반환되는 함수는 다음과 같은 작업을 수행해야 한다.

1. 호출 스로틀링

- 콜백 함수는 즉시 실행되고, `wait` 시간이 지날 때까지 다시 실행되지 않는다. <br />
- `shouldThrottle`이라는 `boolean` 변수로 상태를 관리한다. <br />
- `Idle` 상태에서 함수가 호출되면 <br />
  a) `shouldThrottle`을 `true`로 설정한다. (`Active` 상태가 됨) <br />
  b) `func`를 적절한 인자와 함께 실행한다. <br />
  c) `setTimeout`으로 `wait` 시간 후에 잠금 해체한다. <br />
- 잠금이 활성화된 동안에는 `shouldThrottle` 체크로 인해 `func`가 실행되지 않는다.

2. 적절한 인자와 함께 `func` 실행

- 스로틀된 함수는 원본 함수처럼 사용되어야 한다. <br />
- `this`와 함수 인자들을 원본 콜백 함수 호출 시에 전달해야 한다.

`this` 참조 관련 주의사항: <br />
화살표 함수는 `this`의 렉시컬 바인딩으로 인해 내부 함수 선언에 사용할 수 없다. <br />
`func(...args)`와 같은 직접 호출은 올바른 `this` 참조를 전달하지 않아 사용할 수 없다. <br />
`Function.prototype.apply()` 또는 `Function.prototype.call()`을 사용한다. <br />
`func.apply(thisArg, args)` 혹은 `func.call(thisArg, ...args)`를 사용한다.

---

```javascript
/**
 * @callback func
 * @param {number} wait
 * @return {Function}
 */
export default function throttle(func, wait) {
  let shouldThrottle = false;

  return function (...args) {
    if (shouldThrottle) return;

    shouldThrottle = true;
    setTimeout(() => {
      shouldThrottle = false;
    }, wait);
    func.apply(this, args);
  };
}
```
