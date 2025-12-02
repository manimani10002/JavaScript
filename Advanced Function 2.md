## advanced-function2: 함수, 이벤트, 반복의 현대적인 활용

### 1\. ➡️ 화살표 함수 (Arrow Function)

화살표 함수는 **함수를 간결하게 작성**하기 위해 ES6에서 도입된 문법이며, 특히 콜백 함수를 사용할 때 코드를 훨씬 깔끔하게 만듭니다.

#### 개념 및 문법

- **간결성:** `function` 키워드 대신 화살표 `=>`를 사용합니다.
- **자동 반환:** 함수 본문이 한 줄이고 `return`만 있다면, 중괄호 `{}`와 `return`을 생략할 수 있습니다.
- **`this` 고정 (Lexical `this`):** 가장 중요한 특징으로, 화살표 함수는 자신이 정의된 \*\*외부 환경의 `this`\*\*를 그대로 가져와 사용합니다. 이 덕분에 `this` 값이 예상치 않게 바뀌는 혼란을 방지할 수 있습니다.

#### 코드 예시

```javascript
// 1. 기본 형식
const arrowFunction = () => {
  console.log('hello');
};
arrowFunction(); // 함수 실행

// 2. 이벤트 리스너 콜백 함수로 활용 (가장 일반적인 용례)
buttonElement.addEventListener('click', () => {
  console.log('클릭2');
});
```

---

### 2\. 👂 이벤트 리스너 (`addEventListener`)

이벤트 리스너는 웹 페이지의 특정 요소에서 발생하는 사건(이벤트)을 감지하고, 그 사건이 발생했을 때 JavaScript 함수(콜백 함수)를 실행하여 웹 페이지를 **상호작용적**으로 만듭니다.

#### 기본 구문 및 작동 방식

`addEventListener`는 두 개의 필수 인자를 받습니다.

1.  **이벤트 타입:** 감지할 이벤트의 종류 (예: `'click'`, `'keydown'`).
2.  **리스너 함수:** 이벤트 발생 시 실행할 **콜백 함수**.

<!-- end list -->

```javascript
// 1. DOM 요소 선택
const buttonElement = document.querySelector('.js-button');

// 2. 리스너 함수를 변수에 할당 (제거를 위해 필수!)
const eventListener = () => {
  console.log('click');
};

// 3. 리스너 등록: 'click' 이벤트 발생 시 eventListener 함수 실행 예약
buttonElement.addEventListener('click', eventListener);
```

#### 리스너 제거 (`removeEventListener`)의 중요성

불필요한 동작이나 메모리 낭비를 막기 위해 등록된 리스너를 제거할 수 있습니다.

- **제거 성공 조건:** 등록할 때 사용했던 \*\*함수와 동일한 참조(Reference)\*\*를 `removeEventListener`에 전달해야 합니다.

<!-- end list -->

```javascript
// 등록된 함수 참조를 사용하여 정확하게 리스너 제거
buttonElement.removeEventListener('click', eventListener);
```

- **익명 함수 문제:** `addEventListener('click', () => { ... })`와 같이 익명 함수로 등록하면, 이 함수를 변수에 저장하지 않았기 때문에 나중에 `removeEventListener`로 제거할 수 없습니다. 따라서 **제거할 필요가 있는 리스너**는 반드시 **변수에 할당**하여 사용해야 합니다.

---

### 3\. ♻️ 배열 순회 (`forEach`)

`forEach()`는 배열의 모든 요소를 순회하며 각 요소에 대해 지정된 콜백 함수를 실행하는 **배열 전용 메서드**입니다. `for` 루프를 대체하는 현대적인 방법입니다.

#### 구문 및 인자

`forEach()`는 인자로 **콜백 함수** 하나를 받으며, 이 콜백 함수는 배열의 요소 수만큼 반복 실행됩니다.

```javascript
const arr = [1, 2, 3];

// forEach는 콜백 함수에 value와 index를 자동으로 전달합니다.
arr.forEach((value, index) => {
  console.log(`인덱스 ${index}의 값은 ${value}입니다.`);
});
```

| 인자        | 역할                                         |
| :---------- | :------------------------------------------- |
| **`value`** | 현재 순회 중인 **배열 요소의 값**            |
| **`index`** | 현재 순회 중인 **배열 요소의 인덱스** (위치) |

#### `for` 루프와의 차이점

- `forEach()`는 `for` 루프보다 코드가 간결하고 가독성이 높습니다.
- 가장 큰 차이는 **반복 제어**입니다. `forEach()`는 반복 중에 `break`나 `continue`를 사용하여 **중단하거나 건너뛸 수 없습니다**. 따라서 단순히 배열의 모든 요소에 대해 작업을 실행할 때 유용합니다.
