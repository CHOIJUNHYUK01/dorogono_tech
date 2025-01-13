# Filter

Array의 filter함수를 직접 구성해봄. <br/>
prototype 메서드이기에, this를 사용해서 호출한 배열을 알 수 있음.

### Object.hasOwn()

확인할 배열을 첫 번째 요소로 받음.<br/>
두 번째 요소로 인덱스 혹은 String 이름, 테스트할 속성의 Symbol 값을 받음. <br/>
해당 값이 truthy라면, true를 반환함. <br/>
없다면 false임.

### function.call 과 function.apply

둘 다 함수를 실행한다는 행동은 같음. <br/>
인자를 받는 방식이 다름.

call은 각 인수를 구분해서 받음. <br/>
apply는 각 인수를 배열로만 받음.

### this

Array.prototype 이기에 해당 Array를 가리키고 있음. <br/>
callbackFn에서 사용하는 첫 번째 인자, thisArg는 다름. <br/>
thisArg에 할당된 값을 this로 삼아서 함수를 실행함. <br/>
이 값이 없다면, 전역 객체를 사용해서 함수를 실행함.

```javascript
/**
 * @template T
 * @param { (value: T, index: number, array: Array<T>) => boolean } callbackFn
 * @param {any} [thisArg]
 * @return {Array<T>}
 */
Array.prototype.myFilter = function (callbackFn, thisArg) {
  const ret = [];
  const len = this.length;

  for (let i = 0; i < len; i++) {
    const v = this[i];

    if (Object.hasOwn(this, i) && callbackFn.call(thisArg, v, i, this)) {
      ret.push(v);
    }
  }

  return ret;
};
```
