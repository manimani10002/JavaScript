## 💡 JavaScript 고급 함수 및 비동기 처리 TIL

오늘 학습한 내용은 JavaScript의 핵심인 \*\*함수(Function)\*\*를 \*\*값(Value)\*\*으로 다루는 방식과, 웹 개발에서 필수적인 **비동기(Asynchronous) 코드**의 기본 원리이다.

### 1\. 🥇 함수는 값이다 (First-Class Functions)

JavaScript에서 함수는 숫자나 문자열처럼 **일급 객체**로 취급된다. 이 말은 함수를 다른 값처럼 다룰 수 있다는 의미이다.

#### 1.1. 함수 표현식과 메서드

- **함수 표현식:** 함수를 만들어서 변수에 할당하는 방식. 함수 이름은 생략하고 변수 이름으로 함수를 실행한다.
  ```javascript
  // 함수를 '값'으로 function1 변수에 할당
  const function1 = function greeting() {
    console.log('hello2');
  };
  function1();
  ```
- **메서드:** 함수가 객체의 속성 값으로 저장될 때, 이를 \*\*메서드(Method)\*\*라고 부른다.
  ```javascript
  const object1 = {
    fun: function greeting() {
      // fun은 object1의 메서드
      console.log('hello3');
    },
  };
  object1.fun();
  ```

#### 1.2. 함수를 인자로 전달 (콜백 함수)

함수를 다른 함수를 호출할 때 인자(parameter)로 전달할 수 있다. 이 전달된 함수를 \*\*콜백 함수(Callback Function)\*\*라고 하는데 이는 비동기 처리의 기본 메커니즘이 된다.

```javascript
// run 함수는 인자로 받은 함수(param)를 실행
function run(param) {
  param();
}

// run 함수에 익명 함수(콜백 함수)를 인자로 전달
run(function () {
  console.log('hello4');
});
```

---

### 2\. ⏳ 비동기 코드 및 타이머 함수

JavaScript는 기본적으로 \*\*동기적(순서대로)\*\*으로 실행되지만, 시간이 오래 걸리는 작업(타이머, 네트워크 통신 등)은 **비동기적**으로 처리되어 메인 코드를 막지 않는다.

#### 2.1. 비동기 타이머 함수

`setTimeout`과 `setInterval`은 콜백 함수와 시간을 받아 비동기적으로 실행을 예약하는 웹 API 함수이다.

| 함수                | 역할                                                        | 코드 예시                      | 비고                                            |
| :------------------ | :---------------------------------------------------------- | :----------------------------- | :---------------------------------------------- |
| **`setTimeout()`**  | `delay` 밀리초 **후**에 콜백 함수를 **단 한 번** 실행       | `setTimeout(콜백함수, 3000);`  | 예약 후 즉시 다음 코드로 넘어감                 |
| **`setInterval()`** | `delay` 밀리초 **간격**으로 콜백 함수를 **반복적**으로 실행 | `setInterval(콜백함수, 2000);` | 반복을 멈추려면 `clearInterval()`을 사용해야 함 |

**실행 순서 예시:**

```javascript
setTimeout(function () {
  console.log('timeOut');
}, 3000);

console.log('next line'); // setTimeout의 3초를 기다리지 않고 즉시 실행
```

**`setInterval()` 중지 예시:**

```javascript
let count = 0;
// 인터벌 ID를 저장하여 중지할 때 사용
const intervalId = setInterval(function () {
  count++;
  console.log(`반복 횟수: ${count}`);

  if (count >= 5) {
    clearInterval(intervalId); // 5번 후 반복 중지
    console.log('반복 중지됨');
  }
}, 1000); // 1초 간격으로 반복
```
