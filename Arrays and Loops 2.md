# 📘 TIL — JavaScript + DOM + 배열 + 반복문 + break/continue

## 1. 📌 DOM 조작 기본 개념

브라우저 화면의 요소를 선택하고 값 읽기/쓰기/수정하는 방식.

### ✔ 요소 선택

```js
const input = document.querySelector('.todo-input');
```

### ✔ 값 읽기

```js
const text = input.value;
```

### ✔ 값 변경

```js
document.querySelector('.todo-list').innerHTML = '<p>내용 변경</p>';
```

---

## 2. 📌 이벤트 처리 (`onclick`)

버튼 클릭하면 특정 함수를 실행하도록 연결.

```html
<button onclick="addTodo()">Add</button>
```

```js
function addTodo() {
  console.log('버튼 클릭됨!');
}
```

---

## 3. 📌 배열(Array)에 객체 저장하기

여러 개의 할 일을 관리하기 위해 배열 사용.

```js
const todos = [];

todos.push({
  title: '코딩하기',
  date: '2025-01-01'
});
```

---

## 4. 📌 배열 반복하며 HTML 만들어 화면 렌더링하기

반복문으로 배열 내용을 HTML 문자열로 생성 → `.innerHTML`로 화면에 표시.

```js
function render() {
  let html = '';

  for (let i = 0; i < todos.length; i++) {
    html += `
      <div>${todos[i].title}</div>
      <div>${todos[i].date}</div>
      <button onclick="removeTodo(${i})">Delete</button>
    `;
  }

  document.querySelector('.todo-list').innerHTML = html;
}
```

---

## 5. 📌 Todo 추가하기 (Add 함수 개념)

### 동작 순서

1. input에서 값 가져오기
2. 값 검증
3. 배열에 객체 형태로 저장
4. 화면 리렌더링
5. input 초기화

### 예시 코드

```js
function addTodo() {
  const title = document.querySelector('.todo-input').value;
  const date = document.querySelector('.todo-date').value;

  if (!title || !date) {
    alert('값을 입력해주세요!');
    return;
  }

  todos.push({ title, date });

  render();

  document.querySelector('.todo-input').value = '';
  document.querySelector('.todo-date').value = '';
}
```

---

## 6. 📌 Todo 삭제하기 (splice 사용)

특정 index의 요소 제거 → 다시 렌더링

```js
function removeTodo(index) {
  todos.splice(index, 1);
  render();
}
```

---

## 7. 📌 CSS Grid 개념

입력칸·버튼·Todo 목록을 정렬하기 위한 Grid 사용.

```css
.todo-grid {
  display: grid;
  grid-template-columns: 200px 150px 100px;
  gap: 10px;
}
```

---

## 8. 📌 `break` & `continue` 개념 정리

### ✔ **break**

반복문을 **즉시 종료**시킴.

```js
for (let i = 1; i <= 10; i++) {
  if (i === 5) break;
  console.log(i); 
}

// 출력: 1 2 3 4
```

### ✔ **continue**

이번 반복만 **건너뛰고**, 다음 반복으로 진행.

```js
for (let i = 1; i <= 5; i++) {
  if (i === 3) continue;
  console.log(i);
}

// 출력: 1 2 4 5
```

### ✔ Todo 예시에서 활용 가능성

* 이미 같은 날짜에 todo가 있으면 추가 막기 (continue 사용)
* 첫 번째로 조건 만족하는 todo 찾고 반복 종료하기 (break 사용)
