# Promise.all

input으로 주어진 값을 순회해서, 하나의 `Promise`를 반환한다. <br />
모든 것이 `resolve`되면, `resolve`값을 반환한다. <br />
만약 하나라도 `reject`된다면, `reject`값을 반환한다.

### 잊지 말아야 할 것

1. `Promise`는 연쇄적으로 연결되어있다. 함수는 `Promise`를 반환해야 한다. <br />
2. 입력 배열이 비어있다면, 반환되는 `Promise`는 빈 배열로 `resolve`된다. <br />
3. 모든 `Promise`가 성공적으로 이행(fulfilled)되면, 반환되는 `Promise`는 입력 순서와 동일한 순서로 `resolve`된 값 배열을 포함해야 한다. <br />
4. 입력값 중 하나라도 `reject`되거나 에러를 발생시킨다면, 반환되는 `Promise`는 즉시 `reject`된다. <br />
5. 입력 배열은 `Promise`가 아닌 값도 포함할 수 있다.

## 해결책 1. async를 사용해 unresolve인 Promise를 센다.

함수가 `Promise`를 반환해야 하기에, `Promise`를 함수 상단에 생성하고, 반환해야 한다. <br />
대부분의 코드는 생성자 매개변수 내에 작성될 거다.

먼저 입력 배열이 비어있는지 확인하고, 비어있다면 빈 배열로 `resolve`한다.

그 다음 입력 배열의 모든 항목을 `resolve`하려고 시도해야 한다. <br />
이는 `Array.prototype.forEach` 또는 `Array.prototype.map`을 사용해 달성할 수 있다. <br />
반환된 값들이 입력 배열의 순서를 유지해야 하므로, result 배열을 생성해 입력 배열 내의 인덱스를 사용하여 적절한 위치에 값을 넣는다. <br />
모든 입력 배열 값이 `resolve`되었는지 알기 위해, `resolve`되지 않은 `promise` 개수를 추적한다. <br />
이를 위해 `resolve`되지 않은 값의 카운터를 초기화하고, 값이 `resolve`될 때마다 감소시킨다. <br />
해당 카운터가 0이 됐을 때, result 배열을 반환한다.

여기서 주목할 점은 입력 배열이 `Promise`가 아닌 값을 포함할 수 있다는 거다. <br />
즉, await를 사용하지 않는 경우 각 값을 `Promise.resolve()`로 감싸야 한다. <br />
이렇게 하면 각각에 대해 `.then()`을 사용할 수 있다. <br />
그러면 이제 `Promise`와 `non-Promise` 값을 구분할 필요가 없다. <br />
`resolve`가 필요한지 여부도 고려할 필요가 없다.

마지막으로, 값 중 하나라도 `reject`되면, 대기 중인 `Promise`를 기다리지 않는다. <br />
그 즉시 최상위 `Promise`를 `reject`한다.

```javascript
/**
 * @param {Array} iterable
 * @return {Promise<Array>}
 */
export default function promiseAll(iterable) {
  return new Promise((resolve, reject) => {
    const results = new Array(iterable.length);
    let unresolved = iterable.length;

    if (unresolved === 0) {
      resolve(results);
      return;
    }

    iterable.forEach(async (item, index) => {
      try {
        const value = await item;
        results[index] = value;
        unresolved -= 1;

        if (unresolved === 0) {
          resolve(results);
        }
      } catch (err) {
        reject(err);
      }
    });
  });
}
```

## 해결책 2. Promise.then을 사용해 unresolve인 Promise를 센다.

`async/await`를 사용하길 원치 않는 경우에 사용한다.

```javascript
/**
 * @param {Array} iterable
 * @return {Promise<Array>}
 */
export default function promiseAll(iterable) {
  return new Promise((resolve, reject) => {
    const results = new Array(iterable.length);
    let unresolved = iterable.length;

    if (unresolved === 0) {
      resolve(results);
      return;
    }

    iterable.forEach((item, index) => {
      Promise.resolve(item).then(
        (value) => {
          results[index] = value;
          unresolved -= 1;

          if (unresolved === 0) {
            resolve(results);
          }
        },
        (reason) => {
          reject(reason);
        }
      );
    });
  });
}
```

`Promise`의 해결 함수(resolve || reject) 중 하나라도 호출되면, 해당 `Promise`는 "settled(확정)" 상태가 된다. <br />
이후에 추가적으로 `resolve`나 `reject`함수를 호출되더라도, "fulfillment" 값을 변경할 수 없다. <br />
"rejection" 이유를 변경할 수도 없다. <br />
"fulfilled" 상태에서 "rejected" 상태로 변경이 불가능하다.

쉽게 말하면, `Promise`가 한 번 확정되면, 그 결과는 불변이다. <br />
어떤 방법으로도 변경할 수 없다는 것이다. <br />
이는 `Promise`의 중요한 특성 중 하나로, 결과의 신뢰성과 예측 가능성을 보장한다.
