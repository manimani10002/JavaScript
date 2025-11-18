## 📘 JavaScript Objects & LocalStorage

## 1\. 객체 (Object) 기본 구조 및 조작

자바스크립트 객체는 **Key-Value 쌍**으로 데이터를 저장하는 기본적인 구조다.

### 기본 구조

```javascript
const object1 = {
  name: '태현', // Key: name, Value: '태현'
  age: 28, // Key: age, Value: 28
  // 함수도 값으로 저장 가능 (이것을 '메서드'라 함)
  greet: function greeting() {
    console.log('hello');
  },
};
```

### 객체 조작 방법

| 기능                 | 코드                        | 설명                                         |
| :------------------- | :-------------------------- | :------------------------------------------- |
| **값 수정**          | `object1.name = '박태현';`  | 기존 키의 값을 새로운 값으로 수정.           |
| **새로운 속성 추가** | `object1.hobby = 'coding';` | 존재하지 않는 키에 값을 할당하면 추가.       |
| **속성 삭제**        | `delete object1.age;`       | `delete` 연산자를 사용하여 속성 자체를 제거. |

---

## 2\. 객체 사용법 및 접근

### 값 접근 및 메서드 실행

```javascript
// Dot Notation (점 표기법)으로 값 접근
console.log(object1.name); // '박태현'

// Bracket Notation (대괄호 표기법)으로 값 접근 (동적 Key 접근 시 사용)
console.log(object1['age']); // 28

// 메서드 실행
object1.greet(); // console에 'hello' 출력
```

---

## 3\. LocalStorage 사용법 (객체 저장)

LocalStorage는 브라우저에 데이터를 **문자열** 형태로 영구적으로 저장하는 웹 스토리지 API이다.

| 기능              | 코드                               | 설명                                               |
| :---------------- | :--------------------------------- | :------------------------------------------------- |
| **저장**          | `localStorage.setItem(key, value)` | Key와 Value를 문자열로 저장.                       |
| **불러오기**      | `localStorage.getItem(key)`        | Key에 해당하는 문자열 값을 반환.                   |
| **삭제**          | `localStorage.removeItem(key)`     | 특정 Key의 데이터를 삭제.                          |
| **객체 → 문자열** | `JSON.stringify(object)`           | 객체를 저장하기 위해 JSON 문자열로 변환.           |
| **문자열 → 객체** | `JSON.parse(string)`               | LocalStorage에서 불러온 문자열을 다시 객체로 변환. |

---

## 4\. 실제 사용 예시 코드 (가위바위보 Score 저장)

LocalStorage를 사용하여 게임 점수(`score` 객체)를 유지하고 관리하는 예시코드.

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>rock-paper-scissors</title>
  </head>
  <body>
    <p>Rock Paper Scissors</p>
    <button onclick="myPick = 'rock'; createComputerPick(); rpsResult()">
      Rock
    </button>
    <button onclick="myPick = 'paper'; createComputerPick(); rpsResult()">
      Paper
    </button>
    <button onclick="myPick = 'scissors'; createComputerPick(); rpsResult()">
      Scissors
    </button>

    <button
      onclick="
        score.wins = 0;
        score.losses = 0;
        score.draws = 0;

        // 메모리 초기화 후 LocalStorage에서도 'score' 데이터를 완전히 제거
        localStorage.removeItem('score'); 

        alert(`wins: ${score.wins}\nlosses: ${score.losses}\ndraws: ${score.draws}`)
      "
    >
      Reset Score
    </button>

    <script>
      let myPick;
      let computerPick;

      // LocalStorage에서 'score'를 불러옴. 데이터가 없으면 기본값(0, 0, 0)을 사용.
      const score = JSON.parse(localStorage.getItem('score')) || {
        wins: 0,
        losses: 0,
        draws: 0,
      };

      function createComputerPick() {
        const randomNuber = Math.random();

        if (randomNuber < 1 / 3) {
          computerPick = 'rock';
        } else if (randomNuber < 2 / 3) {
          // 1/3 이상 2/3 미만
          computerPick = 'paper';
        } else {
          // 2/3 이상
          computerPick = 'scissors';
        }
      }

      function rpsResult() {
        let result;

        if (myPick === computerPick) {
          result = 'draw';
        } else if (
          (myPick === 'rock' && computerPick === 'scissors') ||
          (myPick === 'scissors' && computerPick === 'paper') ||
          (myPick === 'paper' && computerPick === 'rock')
        ) {
          result = 'win';
        } else {
          result = 'lose';
        }

        // 1. 메모리의 score 객체 업데이트
        if (result === 'win') {
          score.wins += 1;
        } else if (result === 'lose') {
          score.losses += 1;
        } else {
          score.draws += 1;
        }

        // 2. 변경된 score 객체를 LocalStorage에 문자열로 다시 저장 (업데이트)
        localStorage.setItem('score', JSON.stringify(score));

        alert(
          `myPick: ${myPick}\ncomputerPick: ${computerPick}\nresult: ${result}\nWins: ${score.wins}, Losses: ${score.losses}, Draws: ${score.draws}`
        );
      }
    </script>
  </body>
</html>
```

---

## 5\. `null` vs `undefined`

이 둘은 모두 \*\*"값이 없다"\*\*는 의미를 나타내지만, 그 *상황*과 *의도*가 다름.

- **`undefined`**: **값이 할당되지 않은** 상태.
  - 변수를 선언만 하고 초기화하지 않았을 때.
  - 객체의 존재하지 않는 속성에 접근할 때.
  - 함수가 `return` 문 없이 종료될 때의 반환 값.
- **`null`**: **의도적으로** 값이 없음을 나타내는 상태.
  - 개발자가 "이 변수에는 의도적으로 빈 값을 넣겠다"고 명시적으로 할당한 값.
  - `typeof null`은 버그로 인해 `'object'`가 나옴.

---

## 6\. 객체 선언 개념 (메모리) 및 Reference (참조)

자바스크립트에서 객체는 \*\*참조 타입(Reference Type)\*\*입니다.

1.  **메모리 저장**: 객체(`{...}`)는 메모리의 **힙(Heap)** 영역에 저장됩니다.
2.  **변수 저장**: `const`나 `let`으로 선언된 변수에는 객체 자체가 아니라, 힙에 저장된 객체의 \*\*메모리 주소 (참조, Reference)\*\*만 저장됩니다.

<!-- end list -->

```javascript
const objA = { value: 10 };
const objB = objA; // 객체 자체를 복사하는 것이 아니라, objA가 가진 '참조 주소'를 objB에 복사합니다.

objB.value = 20; // objB가 참조하는 메모리 위치의 값을 변경

console.log(objA.value); // 출력: 20 (objA도 같은 메모리 주소를 가리키므로 값이 바뀜)
```
