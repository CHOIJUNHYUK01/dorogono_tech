# DeepClone

## JSON.stringify

가장 수운 방법이다. <br />
직렬화를 하고, 그 값을 다시 역직렬화한다.

```javascript
export default function deepClone(value) {
  return JSON.parse(JSON.stringify(value));
}
```

`null`, `boolean`, `number`, `string` 모두 포함하는 방식이다. <br />
하지만 주의해야 할 점도 있다.

- `Symbol`을 키로 사용하는 속성은 복사 불가능 <br />
- JSON이 지원하는 값을 가진 속성만 복사 가능 <br />
- 지원되지 않는 데이터 타입은 단순히 무시

### stringify의 특이한 동작

- Date 객체를 ISO 타임스탬프 문자열로 변환 <br />
- NaN과 Infinity는 null로 변환 <br />
- 기타 예상치 못한 동작들이 있음

---

## 재귀 사용

```javascript
/**
 * @template T
 * @param {T} value
 * @return {T}
 */
export default function deepClone(value) {
  if (typeof value !== "object" || value === null) {
    return value;
  }

  if (Array.isArray(value)) {
    return value.map((item) => deepClone(item));
  }

  return Object.fromEntries(
    Object.entries(value).map(([key, value]) => [key, deepClone(value)])
  );
}
```

### 객체 순회

1. `for ... in` 문 사용 <br />
   전통적인 방식으로 키를 순회 <br />
   상속된 열거 가능한 속성도 처리됨

2. Object 메서드 사용 <br />
   `Object.keys()` 키의 배열로 변환 <br />
   `Object.entries()` 키-값 쌍의 배열로 변환 <br />
   둘 다 객체에 직접 정의된 속성만 다룬다.

### 제한 사항

1. 열거 불가능한 속성과 `Symbol` 키를 가진 속성은 무시된다. <br />
2. 속성 설명자가 복제된 객체에 반영되지 않는다. <br />
3. 순환 참조가 있는 경우 <br />
   a. 현재 솔루션은 작동하지 않음 <br />
   b. 무한 루프로 인한 스택 오버플로우 발생 <br />
4. 프로토타입이 복사되지 않음

---

## structuredClone API

브라우저가 가진 native 기능이다. <br />
깊은 복사가 기본적으로 지원된다.

[관련 문서](https://web.dev/articles/structured-clone?hl=ko)
