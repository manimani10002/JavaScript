## 📘 Arrays, Loops, 그리고 Todo List 구현

-----

오늘은 JavaScript의 핵심 구조인 **배열(Arrays)** 과 **반복문(Loops)** 을 학습하고, 이들을 결합하여 웹 애플리케이션의 기본 작동 원리를 보여주는 **Todo List** 기능을 구현했다.

### 1\. 📂 배열 (Arrays) 개념

배열은 여러 데이터를 **순서대로** 저장하는 자료 구조이다.

  * **선언:** 대괄호 `[]`를 사용
  * **인덱스:** 배열의 각 요소는 `0`부터 시작하는 **인덱스**로 접근 (예: `todoList1[0]`)
  * **추가:** 배열의 맨 끝에 요소를 추가할 때는 **`.push()`** 메서드를 사용
  * **삭제:** 특정 index부터 삭제 때는 **`.splice(타겟인덱스, 삭제할 갯수)`** 메서드를 사용

<!-- end list -->

```javascript
const todoList1 = []; 
todoList1.push('공부하기'); // todoList1은 ['공부하기']가 된다.
```

-----

### 2\. 🔁 반복문 (Loops)

반복문은 배열과 같은 데이터 구조를 순회하거나 특정 코드를 반복 실행할 때 사용

#### 1\. `for` 루프 (횟수 기반 반복)

배열의 모든 요소를 처음부터 끝까지 순회하는 데 가장 흔하게 사용

```javascript
// for (초기화; 조건; 증가/감소)
for (let i = 0; i < todoList1.length; i++) {
  // i는 0부터 시작하여 배열의 길이 미만까지 1씩 증가
  const todo = todoList1[i]; 
  console.log(todo);
}
```

#### 2\. `while` 루프 (조건 기반 반복)

조건식이 `true`인 동안 코드를 반복 실행. 무한 루프를 방지하기 위해 루프 내에서 조건을 변경하는 코드가 **필수**

```javascript
let counter = 0;
while (counter < 5) {
  console.log(counter);
  counter++; // 조건 변경
}
```

-----

### 3\. 🎯 JavaScript 웹 앱의 3가지 핵심

오늘 구현한 Todo List는 모든 동적 웹 애플리케이션의 기본 흐름을 따른다.

1.  **데이터 저장 (`Save the Data`):** 앱의 현재 상태(State)를 JavaScript 변수(예: `todoList1` 배열)에 저장
2.  **HTML 생성 (`Generate the HTML`):** 저장된 데이터를 기반으로 화면에 표시할 HTML 문자열 생성
3.  **상호작용 구현 (`Make it Interactive`):** 버튼 클릭과 같은 사용자 이벤트에 반응하여 1번 데이터를 업데이트하고 2번 과정을 다시 실행하여 화면을 갱신

#### HTML 생성 상세

데이터 배열을 HTML 문자열로 변환하고 DOM에 삽입하는 과정

```javascript
function renderTodoList() {
  let todoListHtml = ''; 

  // 1. 반복문으로 배열 순회
  for (let i = 0; i < todoList1.length; i++) {
    const todo = todoList1[i];
    // 2. 각 데이터를 템플릿 리터럴로 HTML 문자열 조각 생성
    const html = `<p>${todo}</p>`; 
    // 3. HTML 문자열 누적
    todoListHtml += html;
  }
  
  // 4. DOM에 삽입하여 화면에 렌더링
  document.querySelector('.show-todo-list').innerHTML = todoListHtml;
}
```

-----

### 4\. 🛠️ Todo List 구현 로직

사용자 입력(`input`)을 받아 배열에 추가하고 즉시 화면을 업데이트하는 함수이다.

```javascript
function addHandler() {
  const input = document.querySelector('#todo');
  const value = input.value.trim(); // 1. 입력 값 가져오기 (공백 제거)

  // 입력값이 비어있으면 함수 종료
  if (!value) return; 

  todoList1.push(value); // 2. 데이터 업데이트 (배열에 추가)
  input.value = '';      // 3. 입력창 비우기

  renderTodoList();      // 4. 화면 갱신 (데이터를 기반으로 HTML 재생성 및 DOM 삽입)
}
```
