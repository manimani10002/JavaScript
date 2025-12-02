## 💡 advanced-function2: 화살표 함수, 이벤트, 배열 메서드, 클로저



### 1\. ➡️ 화살표 함수 (Arrow Functions)

화살표 함수는 ES6에서 도입된, 함수를 정의하는 **간결한 문법**입니다. 특히 콜백 함수를 정의할 때 코드를 매우 깔끔하게 만들어 줍니다.

| 형태 | 기본 (`function` 표현식) | **화살표 함수 (Arrow Function)** |
| :--- | :--- | :--- |
| **기본** | `const func = function() { ... };` | `const func = () => { ... };` |
| **단일 반환** | `const add = function(a, b) { return a + b; };` | `const add = (a, b) => a + b;` |

#### 1.1. 화살표 함수의 핵심 특징: `this`의 고정

화살표 함수는 **자신만의 `this`를 가지지 않고**, 함수가 정의된 **가장 가까운 외부 스코프의 `this`를 상속**받습니다 (**Lexical `this`**).

  * **장점:** `this`가 갑자기 바뀌는 복잡한 상황(특히 타이머나 콜백 내부)을 방지하고 예측 가능하게 만듭니다.
  * **주의점:** **객체의 메서드**나 **생성자 함수**처럼 `this`가 동적으로 해당 객체를 가리켜야 할 때는 일반 함수 (`function`)를 사용해야 합니다.

-----

### 2\. 👂 이벤트 리스너 (`.addEventListener()`)

`addEventListener()`는 DOM 요소에 특정 사건(이벤트)이 발생했을 때 실행할 콜백 함수를 등록하는 표준 방법입니다.

#### 2.1. 기본 구문

```javascript
element.addEventListener('event-type', callbackFunction);
```

  * **`event-type`:** 감지할 이벤트 종류 (예: `'click'`, `'keydown'`).
  * **`callbackFunction`:** 이벤트 발생 시 실행될 함수입니다. 주로 **화살표 함수**가 사용됩니다.

#### 2.2. 리스너 제거 (`.removeEventListener()`)

불필요한 동작을 막고 메모리를 관리하기 위해 리스너를 제거할 수 있습니다.

```javascript
const handler = () => { console.log('실행'); };

button.addEventListener('click', handler);
button.removeEventListener('click', handler); // 반드시 등록 시 사용한 '함수 참조'를 사용해야 합니다.
```

> **주의:** 익명 함수 (`() => {}` 형태로 바로 등록한 함수)는 참조를 저장할 수 없어 `removeEventListener`로 제거할 수 없습니다.

-----

### 3\. 🗺️ 배열 반복 및 변환 메서드

JavaScript 배열은 반복문을 대체하고 데이터 조작을 간결하게 하는 강력한 내장 메서드를 제공합니다.

#### 3.1. `.forEach()` (단순 반복)

배열의 모든 요소에 대해 함수를 실행합니다. 반환 값은 없으며, 단순히 배열을 순회할 때 사용됩니다.

```javascript
const arr = [1, 2, 3];
arr.forEach((value, index) => {
    console.log(`값: ${value}`);
});
// (for 루프와 달리 break로 중단할 수 없습니다.)
```

#### 3.2. `.filter()` (조건 필터링)

배열의 각 요소를 순회하며, 콜백 함수가 \*\*`true`\*\*를 반환하는 요소들만 모아 **새로운 배열**로 반환합니다.

```javascript
const numbers = [10, 25, 30];
// 20보다 큰 요소만 필터링
const bigNumbers = numbers.filter(n => n > 20); 
console.log(bigNumbers); // 출력: [25, 30]
```

#### 3.3. `.map()` (요소 변환)

배열의 모든 요소를 순회하며, 콜백 함수가 반환하는 값들을 모아 **새로운 배열**로 반환합니다. 배열의 형태는 유지하면서 각 요소의 값을 변환할 때 사용됩니다.

```javascript
const costs = [100, 200, 300];
// 모든 값에 10%를 더한 새로운 배열 생성
const taxedCosts = costs.map(cost => cost * 1.1); 
console.log(taxedCosts); // 출력: [110, 220, 330]
```

-----

### 4\. 🔒 클로저 (Closure)

클로저는 \*\*"외부 함수가 종료된 후에도, 내부 함수가 외부 함수의 변수에 접근할 수 있는 현상"\*\*이자, 이 내부 함수 자체를 의미합니다.

#### 4.1. 클로저의 원리

JavaScript 함수는 자신이 **선언될 당시**의 환경(스코프)을 기억합니다. 외부 함수가 실행을 마쳐도, 내부 함수가 그 환경 내의 변수(자유 변수)를 계속 참조하고 있다면, 그 변수는 메모리에서 제거되지 않고 유지됩니다.

```javascript
function createCounter() {
  let count = 0; // 👈 이 변수가 클로저에 의해 '캡처'됨
  
  // 내부 함수가 외부 함수의 변수(count)를 참조합니다.
  return function() { 
    count += 1;
    return count;
  };
}

const counter = createCounter(); // createCounter는 실행이 끝났지만...
console.log(counter()); // 출력: 1 (count 변수는 여전히 살아있음)
console.log(counter()); // 출력: 2 (상태가 유지됨)
```

#### 4.2. 클로저의 용도

  * **상태 유지:** 함수가 호출될 때마다 독립적인 상태(예: 위 예시의 `count`)를 유지해야 할 때 사용됩니다.
  * **정보 은닉 (캡슐화):** 외부에서 `count` 변수에 직접 접근하는 것을 막고, 내부 함수를 통해서만 조작하도록 할 수 있어 안전한 코드 작성이 가능합니다.
