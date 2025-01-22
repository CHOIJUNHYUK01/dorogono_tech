# Flatten

중첩된 함수로 들어온 배열을 모두 같은 레벨에 있도록 바꾼다.

### 순회 + shift + unshift

```javascript
/**
 * @param {Array<*|Array>} value
 * @return {Array}
 */
export default function flatten(value) {
  const clonedArr = value.slice();
  const ret = [];

  while (clonedArr.length) {
    const item = clonedArr.shift();
    if (Array.isArray(item)) {
      clonedArr.unshift(...item);
    } else {
      ret.push(item);
    }
  }

  return ret;
}
```

### Array.prototype.some

```javascript
type ArrayValue = any | Array<ArrayValue>;

export default function flatten(value: Array<ArrayValue>): Array<any> {
  // 하나라도 true라면 진행한다.
  while (value.some(Array.isArray)) {
    value = [].concat(...value);
  }

  return value;
}
```

### Array.prototype.reduce

재귀는 콜스택이 넘칠 위험은 있지만, 크롬은 천만까지, firefox는 5천만까지 괜찮다.

```javascript
/**
 * @param {Array<*|Array>} value
 * @return {Array}
 */
export default function flatten(value) {
  return value.reduce(
    (acc, curr) => acc.concat(Array.isArray(curr) ? flatten(curr) : curr),
    []
  );
}
```

### Array.prototype.splice

다 새로운 배열에 값을 담아 반환했다. <br />
이 방식은 파라미터로 받은 값을 그대로 활용한다.

```javascript
type ArrayValue = any | Array<ArrayValue>;

export default function flatten(value: Array<ArrayValue>): Array<any> {
  for (let i = 0; i < value.length; ) {
    if (Array.isArray(value[i])) {
      // 직접 해당 배열을 바꿈
      value.splice(i, 1, ...value[i]);
    } else {
      i++;
    }
  }

  return value;
}
```

### Array.prototype.flatMap

해당 메서드를 재귀로 해결함.

```javascript
type ArrayValue = any | Array<ArrayValue>;

export default function flatten(value: Array<ArrayValue>): Array<any> {
  return Array.isArray(value) ? value.flatMap((item) => flatten(item)) : value;
}
```

### Generator

깊이가 깊다면, 재귀적인 접근은 위험하다. <br />
그래서 각 배열 아이템을 `yield`로 각각 만들어 활용한다. <br />
`generator`는 `lazy`하기에 재귀보다 좋은 접근법이다.

```javascript
/**
 * @param {Array<*|Array>} value
 * @return {Array}
 */
export default function* flatten(value: Array<any>): Array<any> {
  for (const item of value) {
    if (Array.isArray(item)) {
      yield* flatten(item);
    } else {
      yield item;
    }
  }
}
```

### JSON.stringify + Regex

```javascript
type ArrayValue = any | Array<ArrayValue>;

export default function flatten(value: Array<ArrayValue>): Array<any> {
  return JSON.parse("[" + JSON.stringify(value).replace(/(\[|\])/g, "") + "]");
}
```

### toString + split + map

해당 파라미터는 숫자 배열만 준다. <br />
배열을 `toString()`사용하면 해당 값만 나온다.

```javascript
function flattenOnlyNumbers(array) {
  return array
    .toString()
    .split(",")
    .map((numStr) => Number(numStr));
}
```

### Array.prototype.flat

```javascript
export default function flatten(arr) {
  return arr.flat(Infinity); // 더이상 할 게 없을 때까지 진행한다.
}
```
