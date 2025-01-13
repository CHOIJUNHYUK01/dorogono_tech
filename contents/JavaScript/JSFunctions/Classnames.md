# Classnames

classnames를 조건문으로 이루어지거나, 일반 class 이름을 모두 통합하여 뽑아내는 함수를 구현해봤습니다.

### 배운 것

array가 type으로는 object임. <br />
array.join()을 사용해, 각 요소 사이에 원하는 값 대입하여 문자열로 변환 가능.

```javascript
/**
 * @param {...(any|Object|Array<any|Object|Array>)} args
 * @return {string}
 */
export default function classNames(...args) {
  const classes = [];

  args.forEach((arg) => {
    // falsy값 삭제
    if (!arg) {
      return;
    }

    // 각 타입 뽑아내기
    const argType = typeof arg;

    // 스트링 값과 숫자면 받음
    if (argType === "string" || argType === "number") {
      classes.push(arg);
      return;
    }

    // 배열이라면, 각 요소를 대입함
    if (Array.isArray(arg)) {
      classes.push(classNames(...arg));
      return;
    }

    // 배열도 타입으로 따지면 object가 나오기에 배열 확인 후 진행
    if (argType === "object") {
      for (const key in arg) {
        // 각 값이 있고, truthy값만 허용
        if (Object.hasOwn(arg, key) && arg[key]) {
          classes.push(key);
        }
      }

      return;
    }
  });

  // 띄어쓰기로 구분해야 함
  return classes.join(" ");
}
```
