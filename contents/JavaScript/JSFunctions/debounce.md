# Debounce

짧은 시간에 한 이벤트가 여러 번 발생했을 때 해결하는 방법. <br/>
마지막 이벤트가 발생하고, 일정 시간이 흐른 후에 작동 되는 방식. <br/>
즉, 연이어 호출되는 함수 중 마지막 또는 첫 함수만 호출하도록 함.

### 화살표 함수

setTimeout 함수는 비동기 함수임. <br/>
일반 함수와 같은 this를 갖지 않음. <br/>
화살표 함수를 사용하면, 선언된 시점의 렉시컬 스코프의 this를 적용하기에 이를 사용해 간단하게 만듦. <br/>
즉, this를 변경할 수 없음.

일반 function 함수를 사용했다면, 아래와 같음.

```javascript
timeoutID = setTimeout(function () {
  timeoutID = null;
  func.apply(context, args);
}, wait);
```

func.apply 혹은 func.call을 사용해 안전하게 this 값을 같이 전달해서 함수를 실행하게 함.

```javascript
/**
 * @param {Function} func
 * @param {number} wait
 * @return {Function}
 */

// 1. 일정 시간이 흐른 후에 이벤트 발생시키는 함수
// Trailing Debounce
export default function debounce(func, wait) {
  let timerID = null;

  return function (...args) {
    clearTimeout(timerID);

    timerID = setTimeout(() => {
      timerID = null;
      func(args);
    }, wait);
  };
}

// 2. 처음 이벤트 실행 후, 이후 이벤트는 일정 시간 무시
// Leading Debounce
export default function debounce(func, wait) {
    let timerID = null;

    return function(...args) {
        if(timerID) return;

        func(args);
        timerID = setTimeout(() => {
            timerID = null;
        }, wait);
    };
}
```
