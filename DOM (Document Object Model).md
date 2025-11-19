## 🌐 JavaScript DOM (Document Object Model) 기초 가이드

---

DOM은 웹 페이지를 조작하기 위한 자바스크립트의 핵심 개념이다. 쉽게 말해 **"자바스크립트가 HTML을 이해하고 조작할 수 있도록 만든 약속"** 이라고 생각하면 된다.

HTML 문서의 모든 요소(버튼, 문단, 이미지 등)를 **객체(Object)** 형태로 변환해 주며, 이 객체를 통해 웹 페이지의 내용, 스타일, 구조를 마음대로 바꾸거나 새로운 기능을 추가할 수 있다.

### 1\. 🏠 DOM 구조: HTML을 객체로 변환

브라우저는 HTML 파일을 읽어 들일 때, 모든 요소를 **나무(Tree) 모양의 구조** 로 만든다. 이 구조를 DOM이라고 한다.

- `document`: 웹 페이지 전체를 의미
- `document.body`: `<body>` 태그를 나타내는 객체
- `document.title`: `<title>` 태그의 내용을 나타냄

**예시 코드:**

```javascript
// 현재 웹 페이지의 제목을 'Good job!'으로 변경
document.title = 'Good job!';

// body 태그 안에 있는 모든 내용을 새로운 내용으로 완전히 대체
document.body.innerHTML = '<h1>DOM 조작 완료!</h1>';
```

---

### 2\. 🔍 원하는 요소 찾기: `document.querySelector()`

웹 페이지의 특정 부분을 바꾸려면, 먼저 그 부분을 **정확하게 찾아야** 한다. `querySelector()` 메서드는 CSS에서 요소를 선택하는 방법과 똑같이 사용하여 요소를 찾는다.

| 선택 방법       | CSS 문법       | JavaScript 코드                          |
| :-------------- | :------------- | :--------------------------------------- |
| **태그 이름**   | `button`       | `document.querySelector('button')`       |
| **클래스 이름** | `.js-button`   | `document.querySelector('.js-button')`   |
| **ID 이름**     | `#main-header` | `document.querySelector('#main-header')` |

**예시 코드:**

```html
<button class="js-button">두 번째 버튼</button>
```

```javascript
// 'js-button' 클래스를 가진 첫 번째 <button> 객체를 찾아서 변수에 저장
const myButton = document.querySelector('.js-button');

// 찾은 버튼의 텍스트를 '클릭됨'으로 변경
myButton.innerHTML = '클릭됨';
```

---

### 3\. ✍️ 내용 확인 및 수정: `.innerHTML` vs `.value`

요소를 찾았다면, 그 내용을 읽거나 수정할 수 있습니다. 어떤 속성을 사용할지는 요소의 종류에 따라 달라집니다.

| 속성             | 용도                                                                  | 예시 요소                                            |
| :--------------- | :-------------------------------------------------------------------- | :--------------------------------------------------- |
| **`.innerHTML`** | **태그와 태그 사이**의 HTML 콘텐츠를 읽거나 씀                        | `<p>여기가 내용</p>`, `<button>여기가 내용</button>` |
| **`.value`**     | `<input>`이나 `<textarea>` 같은 **사용자 입력 필드의 값**을 읽거나 씀 | `<input type="text" value="이 값">`                  |

**예시 코드:**

```html
<input type="text" class="js-input" />
```

```javascript
const inputElement = document.querySelector('.js-input');

// 1. input의 현재 값을 가져와서 출력
console.log(inputElement.value); // (사용자가 입력한 내용)

// 2. input에 새로운 기본값을 설정
inputElement.value = '여기에 이름을 입력하세요';
```

---

### 4\. 🔢 입력 값은 항상 문자열: `Number()`의 중요성

웹에서 사용자로부터 받은 모든 입력 값(`.value`로 가져온 값)은 기본적으로 **문자열(string)** 이다. 숫자로 계산을 하려면 반드시 `Number()` 함수를 사용하여 숫자 타입으로 변환해야 한다.

```javascript
const num1 = '10'; // 사용자 입력 (문자열)
const num2 = 5; // 자바스크립트 숫자

// 변환 없이 덧셈: 문자열 연결이 발생!
console.log(num1 + num2); // 출력: "105"

// 변환 후 덧셈: 올바른 숫자 계산이 됨
console.log(Number(num1) + num2); // 출력: 15
```

---

### 5\. 👂 이벤트 리스너: 반응하는 웹 만들기

**이벤트 리스너(Event Listener)** 는 웹 페이지에서 일어나는 특정 사건(이벤트)을 감지하고, 그 사건이 발생했을 때 **특정 코드(함수)** 를 실행하도록 예약하는 기능.

가장 좋은 방법은 `addEventListener`를 사용하는 것이다.

```javascript
// 1. 버튼 요소를 가져옴
const button = document.querySelector('.js-button');

// 2. 버튼에 'click' 이벤트를 감지하도록 리스너를 추가
button.addEventListener('click', function () {
  // 3. 클릭 이벤트가 발생하면 이 코드가 실행
  alert('버튼이 눌렸습니다!');
});

// 키보드 엔터(Enter) 키 입력 이벤트 감지 예시
document.body.addEventListener('keydown', (event) => {
  if (event.key === 'Enter') {
    console.log('엔터키를 눌렀군요!');
  }
});
```

| 자주 사용되는 이벤트 | 설명                                                        |
| :------------------- | :---------------------------------------------------------- |
| **`click`**          | 마우스로 클릭했을 때                                        |
| **`keydown`**        | 키보드 키를 눌렀을 때                                       |
| **`scroll`**         | 화면이 스크롤될 때                                          |
| **`change`**         | `<input>`이나 `<select>`의 값이 변경되고 포커스를 잃었을 때 |
