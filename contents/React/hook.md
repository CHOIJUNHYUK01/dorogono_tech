# Hooks

"use"로 시작하는 다른 모든 함수를 훅이라고 한다. <br />
훅은 React가 오직 "렌더링" 중일 떄만 사용할 수 있는 특별한 함수다. <br />
이를 통해 다양한 React 기능을 연결할 수 있다.

훅은 함수지만, 컴포넌트의 필요에 대한 무조건적인 선언으로 생각하면 된다. <br />
컴포넌트의 최상위 수준 또는 커스텀 훅에서만 호출이 가능하기 때문이다. <br />
조건문, 반복문 또는 기타 중첩 함수 내부에서는 호출이 불가능하다. <br />
모듈을 "import"하는 것과 유사하게, 컴포넌트 상단에서 React 기능을 "사용"한다.

## useState

이를 호출한다는 것은 React 컴포넌트가 무언가를 기억하길 원한다고 말하는 것이다.

### 작동 방식

1. 컴포넌트가 처음 렌더링된다. <br />
   `state` 초기값으로 전달된 값으로 반환한다.

2. `state`를 업데이트한다. <br />
   버튼을 클릭해서 값을 변경한다고 했다면, 그 함수가 `setter` 함수를 실행하고, 변경 값을 기억하게 만든다. <br />
   후에 렌더링을 유발한다.

3. 컴포넌트가 두 번째로 렌더링된다. <br />
   변경된 값을 기억하기에, 변경된 값을 반환한다.

4. 이런 식으로 계속 반복된다.

서로 연관이 없는 여러 `state` 변수를 가질 수 있다. <br />
하지만, 두 개 이상의 변수가 자주 함께 변경된다면, 하나로 합치는 게 더 좋을 수 있다.

`state`는 화면에서 컴포넌트 인스턴스에 지역적이다. <br />
동일한 컴포넌트를 두 번 렌더링한다면, 각 복사본은 완전히 격리된 `state`를 가진다. <br />
그중 하나를 변경해도, 다른 하나에 영향을 주지 않는다.

그래서 `state`를 일반적인 모듈 상단에 선언할 수 있는 보통의 변수와 구별되는 것이다. <br />
이는 특정 함수 호출이나 코드 내의 특정 위치와 관련이 없다. <br />
대신, 화면의 특정 위치에 "지역적"일 뿐이다.

`props`와 달리, `state`는 선언한 컴포넌트에 완전히 비공개다. <br />
부모 컴포넌트도, 형제 컴포넌트, 자식 컴포넌트도 이를 변경할 수 없고, 심지어는 그것이 있는지도 모른다. <br />
이로써 다른 컴포넌트에 영향을 미치지 않고, 어떤 컴포넌트에든 추가하고 제거할 수 있게 된다.

서로 다른 컴포넌트가 동기화되길 원한다면, 가장 가까운 공통 부모 컴포넌트에 추가하는 것이다.

---

### React는 어떤 state를 반환할지 어떻게 알까?

`useState` 호출이 어떤 `state` 변수를 참조하는지에 대한 정보를 받지 못한다. <br />
이에 전달되는 "식별자"가 없는데, 어떤 변수를 반환할지 어떻게 알까? <br />
함수를 파싱하는 것과 같은 마법일까? <br />
답은 "아니오"다.

"훅"은 동일한 컴포넌트의 모든 렌더링에서 안정적인 호출 순서에 의존한다. <br />
"최상위 수준에서만 훅 호출"이란 규치만 따르면, 항상 같은 순서로 호출되기 때문에 잘 작동한다.

내부적으로 React는 모든 컴포넌트에 대해 한 쌍의 `state` 배열을 가진다. <br />
렌더링 전에 0으로 설정된 현재 인덱스 쌍을 유지한다. <br />
`useState`를 호출할 떄마다, React는 다음 `state` 쌍을 제공하고, 인덱스를 증가시킨다.
